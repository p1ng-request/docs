<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_stargazers_from_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+stargazers+from+repository:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #stars #stargazers #naas_drivers #operations #analytics #html #plotly #csv #image #png

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook provides a way to retrieve the list of users who have starred a given GitHub repository and save it into a csv file.

**References:**
- [GitHub - List Stargazers](https://docs.github.com/en/rest/activity/starring?apiVersion=2022-11-28#list-stargazers)
- [Naas drivers - GitHub](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/github.py)

## Input

### Imports


```python
from naas_drivers import github
import naas
```

### Setup Variables
[Create your GitHub personal access token](https://github.com/settings/tokens)
- `token`: GitHub personal access token
- `repo_url`: URL of the GitHub repository
- `csv_output`: CSV output path


```python
# Inputs
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_GITHUB_TOKEN"
repo_url = "https://github.com/jupyter-naas/awesome-notebooks"

# Outputs
csv_output = f"GitHub_{repo_url.split('/')[-1]}_stargazers.csv"
```

## Model

### Get stargazers
Dataframe returned:
- LOGIN: GitHub Login
- ID: GitHub profile ID
- URL: GitHub API profile URL
- TYPE: User type
- SITE_ADMIN: User admin (Boolean)
- STARRED_AT: Starring date


```python
df = github.connect(token).repos.get_stargazers(repo_url)
print('Row fetched:', len(df))
df.tail(3)
```

## Output

### Save dataframe to csv


```python
# Save your dataframe in CSV
df.to_csv(csv_output, index=False)
```
