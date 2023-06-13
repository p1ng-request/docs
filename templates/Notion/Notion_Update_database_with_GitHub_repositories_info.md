<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Update_database_with_GitHub_repositories_info.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Update+database+with+GitHub+repositories+info:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #database #update #github #repositories #automation #scheduler

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook updates a Notion database with information from all repositories within your GitHub organization. The following data will be updated in your Notion database:
- Name: The name of the repository.
- GitHub URL: The URL for the repository on GitHub.
- Description: A brief description of what the repository is for.
- Default branch: The default branch for the repository (i.e., the branch that is checked out when someone first clones the repository).
- Visibility: The visibility status of the repository (e.g., public, private, or internal).
- Created date: The date when the repository was created.
- Last updated date: The date when the repository was last updated.
- Open Issues: The number of unresolved issues (i.e., bug reports, feature requests, or other tasks) in the repository.
- Forks: The number of times the repository has been forked (i.e., copied to another GitHub account).
- Stargazers: The number of GitHub users who have "starred" the repository (i.e., marked it as a favorite).
- Size: The size of the repository in terms of disk space used.

**References:**
- [Notion Drivers](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/notion.py)
- [PyGithub](https://pypi.org/project/PyGithub/)

## Input

### Import libraries


```python
import naas
from naas_drivers import notion
import pandas as pd
import re
from datetime import datetime
import os
import requests
import naas
import github
```

### Setup Variables
[Generate your personal access token](https://github.com/settings/tokens) and add "repo" in your scope.
- `github_token`: GitHub personal access token
- `github_organization`: GitHub organization name

[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `notion_token`: Notion token shared with your database
- `database_key`: Database key name = page title in notion
- `force_update`: By default, the value is set to False, indicating that only dynamic data such as Forks, Stargazers, Open Issues, and Last updated date will be updated.
- `notion_database`: URL of your notion database
- `output_dir`: directory to save data extracted from LinkedIn


```python
# Inputs
github_token = naas.secret.get('GITHUB_TOKEN') or "YOUR_TOKEN"
github_organization = "jupyter-naas"
notion_token = naas.secret.get("NOTION_TOKEN_METRICS") or "YOUR_TOKEN"
database_key = "Name"
force_update = False

# Outputs
notion_database = "https://www.notion.so/naas-official/93377d8407d84b01b26558913ff6b573?v=1122f024d70e4099aa51f70f0fa9b1ae&pvs=4"
output_dir = "/home/ftp/naas-notion-os/outputs/repositories"
```

### Schedule your automation


```python
# Schedule during week days every day at 8:00 PM
naas.scheduler.add(cron="0 20 * * 1-5")

# naas.scheduler.delete() # uncomment and execute cell to delete automation
```

## Model

### Get Notion DB


```python
def create_notion_db(notion_database, key, token):
    # Get database
    database_id = notion_database.split("/")[-1].split("?v=")[0]
    pages = notion.connect(token).database.query(database_id, query={})

    # Init
    df_output = pd.DataFrame()
    
    # Loop on page
    for page in pages:
        # Get page_id
        page_id = page.id
        
        # Create dataframe from page
        df = page.df()
        
        # Remove empty pages
        page_title = df.loc[df.Name == key, "Value"].values[0]
        if page_title == "":
            notion.connect(token).blocks.delete(page_id)
            print(f"Page '{page_id}' empty => removed from database")
        else:
            # Pivot rows to columns
            columns = df["Name"].unique().tolist()
            new_df = df.copy()
            new_df = new_df.drop("Type", axis=1)
            new_df = new_df.T
            for i, c in enumerate(new_df.columns):
                new_df = new_df.rename(columns={c: columns[i]})
            new_df = new_df.drop("Name").reset_index(drop=True)

            # Add page ID
            new_df["PAGE_ID"] = page_id

            # Concat dataframe
            df_output = pd.concat([df_output, new_df])
    return df_output

df_notion = create_notion_db(
    notion_database,
    database_key,
    notion_token
)
print("📊 Notion DB:", len(df_notion))
df_notion.head(1)
```

### List organization repositories

Using the [PyGithub](https://pygithub.readthedocs.io/en/latest/) library, we can list all the repositories of an organization.


```python
# Create a Github instance
g = github.Github(github_token)
# Get the organization
org = g.get_organization(github_organization)
# List all the repositories
repos = org.get_repos()
```

## Output

### Update data in Notion


```python
# Get data
database_id = notion_database.split("/")[-1].split("?v=")[0]
for repo in repos:
    # Init
    page_new = False
    page_id = None
    name = repo.name
    print("➡️ Started for:", name)
    
    # Create or get page
    notion_page = df_notion.loc[df_notion["Name"] == name, "PAGE_ID"]
    if len(notion_page) > 0:
        page_id = notion_page.values[0]
        page = notion.connect(notion_token).page.get(page_id)
    else:
        page = notion.connect(notion_token).Page.new(database_id=database_id).create()
        page.title("Name", repo.name)
        page_new = True
        
    # Update static data
    if page_new or force_update:
        page.date("Created date", repo.created_at.strftime("%Y-%m-%d"))
        page.link("GitHub url", repo.html_url)
        page.select("Default branch", repo.default_branch)
        page.select("Visibility", repo.visibility)
        if repo.description:
            page.rich_text("Description", repo.description)
            
    # Update dynamic data
    page.number("Stargazers", repo.stargazers_count)
    page.number("Forks", repo.forks_count)
    page.number("Size", repo.size)
    page.number("Open Issues", repo.open_issues)
    page.date("Last updated date", repo.updated_at.strftime("%Y-%m-%d"))
    page.update()
    print(f"✅ Data successfully updated in Notion.")
    
    # Save page to csv
    df = page.df()
    csv_name = f"{datetime.now().strftime('%Y%m%d')}_{name}_info.csv"
    output_path = os.path.join(output_dir, name)
    if not os.path.exists(output_path):
        os.makedirs(output_path)
    csv_path = os.path.join(output_path, csv_name)
    df.to_csv(csv_path, index=False)
    print(f"✅ Data saved to csv:", csv_path)
```
