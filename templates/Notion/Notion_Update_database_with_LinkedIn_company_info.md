<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Update_database_with_LinkedIn_company_info.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Update+database+with+LinkedIn+company+info:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #database #update #linkedin #company #automation #scheduler

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook streamlines the process of updating a Notion database containing company names by extracting relevant information from LinkedIn using Google search, as well as utilizing Naas_Drivers.Notion and Naas_Drivers.LinkedIn.The following data will be updated in your Notion database:
- Name: The name of the company or organization.
- LinkedIn: The company's LinkedIn page.
- Website: The company's website URL.
- Industry: The industry or industries that the company operates in.
- Specialties: The areas of expertise or specialization for the company or its products/services.
- Tagline: A brief statement that summarizes the purpose or mission of the company or organization.
- City: The city or cities where the company is headquartered or operates.
- Country: The country where the company is headquartered or operates.
- Staff Count: The number of employees or staff members employed by the company.
- Staff Range: The range of employee count (e.g., 1-10, 11-50, 51-200, etc.) that the company falls into.
- Followers: The number of LinkedIn users who follow the company's page or profile.

Overall, this notebook can be useful for any business or individual who needs to keep track of company information for various purposes:
- Sales prospecting: Sales teams could use the updated database to identify potential new leads and target them with personalized outreach based on their company information.
- Competitor analysis: Marketers could use the updated database to track changes in their competitors' company information, such as changes in leadership or expansion into new markets.
- Industry research: Researchers could use the updated database to gather information on companies within a particular industry, such as their size, location, and areas of expertise.
- Investor relations: Investors could use the updated database to identify potential investment opportunities and track the performance of companies they are interested in.

**References:**
- [Notion Drivers](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/notion.py)
- [LinkedIn Drivers](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/linkedin.py)

## Input

### Import libraries


```python
import naas
from naas_drivers import linkedin, notion
try:
    from googlesearch import search
except:
    !pip install google
    from googlesearch import search
import re
from datetime import datetime
import os
import requests
import pandas as pd
import time
```

### Setup Variables
[Get your LinkedIn cookies](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)
- `li_at`: LinkedIn cookie used to authenticate Members and API clients 
- `JSESSIONID`: LinkedIn cookie used for Cross Site Request Forgery (CSRF) protection and URL signature validation.

[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `notion_token`: Notion token shared with your database
- `database_key`: Database key name = page title in notion
- `database_linkedin`: Notion property storing the LinkedIn URL
- `force_update`: To be used at 'True' if you want to update the entire dabatase, otherwise it will only update new entries
- `notion_database`: URL of your notion database
- `output_dir`: directory to save data extracted from LinkedIn


```python
# Inputs
li_at = naas.secret.get("LINKEDIN_LI_AT")
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID")
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
database_key = "Name"
database_linkedin = "LinkedIn"
force_update = False

# Outputs
notion_database = "https://www.notion.so/xxxxxxxxxxxx"
output_dir = "organizations"
```

### Schedule your automation


```python
# Schedule during week days every hour between 9:00 AM to 8:00 PM
naas.scheduler.add(cron="0 9-20 * * 1-5")

# naas.scheduler.delete() # uncomment and execute cell to delete automation
```

## Model

### Constants
- `LINKEDIN_PATTERN`: LinkedIn organization pattern to be searched in Google


```python
LINKEDIN_PATTERN = "https:\/\/.+.linkedin.com\/(company|school)\/*([^?])+"
```

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

### Get rows to update
If `force_update` is set to `False`, any rows that have already been updated will be excluded.<br>
In order to determine whether a row has already been updated, we need to check the LinkedIn URL that is set within the LinkedIn column.<br>
Specifically, if the URL begins with https://www.linkedin.com/ and includes "school" or "company" followed by an ID number, it is considered updated because a human would have access to the corresponding organization ID.<br>
It is important to note that the URL must match the LinkedIn pattern for organizations, which is as follows: 'https://.+.linkedin.com/(company|school)/*([^?])+'.


```python
def get_new_rows(
    df,
    linkedin_col,
    force_update,
):
    # Check if df is not empty
    if len(df) == 0:
        return pd.DataFrame()
    
    # Return all rows if force update is True
    if force_update:
        return df
    
    # Check if LinkedIn col exists in df to filter rows
    if linkedin_col in df.columns:
        linkedin_valid = df[
            (df[linkedin_col].str.match(LINKEDIN_PATTERN)) & 
            (df[linkedin_col].str[-1:].str.isnumeric())
        ][linkedin_col].unique()
        df = df[~df[linkedin_col].isin(linkedin_valid)]
    else:
        df[linkedin_col] = None
    return df.reset_index(drop=True)

df_new_rows = get_new_rows(df_notion, database_linkedin, force_update)
print("Rows to update:", len(df_new_rows))
df_new_rows.head(len(df_new_rows))
```

### Get LinkedIn URL
The purpose of this function is to update the LinkedIn URL if it has not been provided with Google Search.<br>
If Google Search does not return any valid URL, we will add this URL by default: https://www.linkedin.com/company/0


```python
# Search LinkedIn in Google
def get_linkedin_url(
    row,
    key,
    linkedin_col,
):
    # Init
    keyword = row[key]
    linkedin_url = row[linkedin_col]
    url = "https://www.linkedin.com/company/0"
    
    # Check if url is valid
    if re.match(LINKEDIN_PATTERN, linkedin_url):
        return linkedin_url
    
    # Create query
    keyword = keyword.replace(" ", "+")
    query = f"{keyword}+Linkedin"
    print("--> Google query:", query)
    
    # Search in Google
    for i in search(query, tld="com", num=10, stop=10, pause=2):
        result = re.search(LINKEDIN_PATTERN, i)

        # Return value if result is not None
        if result != None:
            url = result.group(0).replace(" ", "")
            print("Result found:", url)
            return url
    return url

def udpate_linkedin_url(
    df,
    key,
    linkedin_col,
):
    # Check if df is not empty
    if len(df) == 0:
        return pd.DataFrame()
    else:
        df[linkedin_col] = df.apply(lambda row: get_linkedin_url(row, key, linkedin_col), axis=1)
        return df.reset_index(drop=True)

df_update = udpate_linkedin_url(
    df_new_rows,
    database_key,
    database_linkedin,
)
print("Rows to update:", len(df_update))
df_update.head(len(df_update))
```

## Output

### Update data in Notion


```python
if len(df_update) > 0:
    # Loop to enrich info
    for index, row in df_update.iterrows():
        # Init variables
        name = row[database_key]
        lk_url = row[database_linkedin]
        organization_type = lk_url.split("linkedin.com/")[-1].split("/")[0]
        lk_public_id = lk_url.split(organization_type)[-1].split("/")[1]
        page_id = row["PAGE_ID"]
        print("➡️ Update info for:", name)

        # Get page
        page = notion.connect(notion_token).page.get(page_id)

        # Get LinkedIn Info
        if lk_public_id != "0":
            df = linkedin.connect(li_at, JSESSIONID).company.get_info(lk_public_id)
            df = df.astype(str).replace("None", "")
            org_name = df.loc[0, "COMPANY_NAME"]
            org_id = df.loc[0, "COMPANY_ID"]
            org_url = f"https://www.linkedin.com/{organization_type}/{org_id}"
            org_industry = df.loc[0, "INDUSTRY"]
            org_website = df.loc[0, "WEBSITE"]
            org_desc = df.loc[0, "DESCRIPTION"]
            org_tagline = df.loc[0, "TAGLINE"]
            org_spec = df.loc[0, "SPECIALITIES"]
            org_country = df.loc[0, "COUNTRY"]
            org_city = df.loc[0, "CITY"]
            org_region = df.loc[0, "REGION"]
            org_staff = df.loc[0, "STAFF_RANGE"]
            org_staff_count = df.loc[0, "STAFF_COUNT"]
            org_followers = df.loc[0, "FOLLOWER_COUNT"]
            org_logo_url = df.loc[0, "LOGO_URL"]

            # Save dataframe to csv
            org_name_c = org_name.replace(' ', '_')
            csv_name = f"{datetime.now().strftime('%Y%m%d')}_LINKEDIN_ORGANIZATION_{org_id}.csv"
            output_path = os.path.join(output_dir, org_name_c)
            if not os.path.exists(output_path):
                os.makedirs(output_path)
            csv_path = os.path.join(output_path, csv_name)
            df.to_csv(csv_path, index=False)
            print(f"✅ Data saved to csv:", csv_path)

            # Update Notion Properties
            page.title("Name", str(org_name))
            page.link(database_linkedin, org_url)
            page.number("Staff Count", int(org_staff_count))
            page.number("Followers", int(org_followers))
            page.rich_text("Tagline", str(org_tagline))
            if str(org_staff) != "":
                page.select("Staff Range", str(org_staff))
            if str(org_industry) != "":
                page.select("Industry", str(org_industry))
            if str(org_website) != "":
                page.link("Website", str(org_website))
            if str(org_country) != "":
                page.select("Country", str(org_country))
            if str(org_city) != "":
                page.select("City", str(org_city))
            if org_spec != '[]':
                page.multi_select("Speciliaties", org_spec.split(","))
            page.update()
            print(f"✅ Data successfully updated in Notion.")

            # Update page blocks
            page.heading_2(f"Organization")
            page.heading_3(f"Tagline")
            page.paragraph(org_tagline)
            page.heading_3(f"Description")
            for t in org_desc.split('\n'):
                page.paragraph(t)
            page.update()
            print(f"✅ Description successfully updated in Notion.")

            # Update Logo in page
            if str(org_logo_url) != "None" and org_logo_url.startswith("https://media"):
                notion.client.pages.update(
                    page_id=page.id, icon={"type": "external", "external": {"url": org_logo_url}}
                )
                print(f"✅ Logo successfully updated in Notion.")
                
            # Sleep time
            time.sleep(5)
        else:
            page.link(database_linkedin, lk_url)
            page.update()
            print(f"✅ LinkedIn URL to be updated.")
```

 
