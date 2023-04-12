    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Update_Database_with_LinkedIn_Company_Info.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Update+Database+with+LinkedIn+Company+Info:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #database #update #linkedin #company #info

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook updates a database filled with company name with info found on LinkedIn using google search, naas_drivers.notion and naas_drivers.linkedin.

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
```

### Setup Variables
[Get your LinkedIn cookies](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)
- `li_at`: LinkedIn cookie used to authenticate Members and API clients 
- `JSESSIONID`: LinkedIn cookie used for Cross Site Request Forgery (CSRF) protection and URL signature validation.

[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `notion_token`: Notion token shared with your database
- `database_key_name`: Database key name to be used to create new page
- `force_update`: To be used at 'True' if you want to update the entire dabatase, otherwise it will only update new entries
- `notion_database`: URL of your notion database
- `output_dir`: directory to save company data extracted from LinkedIn


```python
# Inputs
# -> LinkedIn
LI_AT = naas.secret.get("LINKEDIN_LI_AT")
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID")

# -> Notion
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
database_key_name = "Name"
force_update = False

# Outputs
notion_database = "https://www.notion.so/naas-official/341eaeba74224c93adaf5ab51f87f1b2?v=xxxxxxxxxxx"
output_dir = "."
```

### Schedule your automation


```python
# Schedule during week days every hour between 9:00 AM to 8:00 PM
naas.scheduler.add(cron="0 9-20 * * 1-5")

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
    database_key_name,
    notion_token
)
print("📊 Notion DB:", len(df_notion))
df_notion.head(1)
```

## Output

### Get Company Info


```python
def get_linkedin_url(company):
    # Init linkedinbio
    linkedinbio = None
    
    # Create query
    query = f"{company}+Linkedin"
    print("--> Google query:", query)
    
    # Search in Google
    for i in search(query, tld="com", num=10, stop=10, pause=2):
        pattern = "https:\/\/.+.linkedin.com\/company\/.([^?])+"
        result = re.search(pattern, i)

        # Return value if result is not None
        if result != None:
            linkedinbio = result.group(0).replace(" ", "")
            return linkedinbio
    return linkedinbio

for index, row in df_notion.iterrows():
    # Init variables
    google_search = False
    lk_company_url = None
    company_name = row["Name"]
    page_id = row["PAGE_ID"]
    
    # Get page ID
    page = notion.connect(notion_token).page.get(page_id)
    
    # Check if value already exists
    if "Google Search" in df_notion.columns:
        google_search = row["Google Search"]
    if "LinkedIn URL" in df_notion.columns:
        lk_company_url = row["LinkedIn URL"]    
    if str(lk_company_url) == "None" and str(google_search) == "False":
        # Finding URL
        print("🔍 Finding LinkedIn URL for:", company_name)
        lk_company_url = get_linkedin_url(company_name)
        print("--> Result found:", lk_company_url)
            
    if lk_company_url != "None" and lk_company_url is not None:
        if not lk_company_url[-1:].isnumeric() or force_update:
            print("➡️ Update info for:", company_name)
            # Get LinkedIn Company Info
            df_company = linkedin.connect(LI_AT, JSESSIONID).company.get_info(lk_company_url)
            company_name = df_company.loc[0, "COMPANY_NAME"]
            company_id = df_company.loc[0, "COMPANY_ID"]
            company_url = f"https://www.linkedin.com/company/{company_id}"
            company_industry = df_company.loc[0, "INDUSTRY"]
            company_website = df_company.loc[0, "WEBSITE"]
            company_desc = df_company.loc[0, "DESCRIPTION"]
            company_country = df_company.loc[0, "COUNTRY"]
            company_city = df_company.loc[0, "CITY"]
            company_staff = df_company.loc[0, "STAFF_RANGE"]
            company_followers = df_company.loc[0, "FOLLOWER_COUNT"]
            company_logo_url = df_company.loc[0, "LOGO_URL"]

            # Save dataframe
            company_name_c = company_name.replace(' ', '_')
            csv_name = f"{datetime.now().strftime('%Y%m%d')}_LINKEDIN_COMPANY_{company_id}.csv"
            output_path = os.path.join(output_dir, company_name_c)
            if not os.path.exists(output_path):
                os.makedirs(output_path)
            df_company.to_csv(os.path.join(output_path, csv_name), index=False)

            # Update Notion Properties
            page.title("Name", company_name)
            page.link("LinkedIn URL", company_url)
            page.select("Industry", company_industry)
            page.link("Website", company_website)
            page.select("Country", company_country)
            page.select("City", company_city)
            page.select("Staff Range", company_staff)
            page.number("Followers", int(company_followers))
            page.checkbox("Google Search", True)
            if company_logo_url != "None":
                notion.client.pages.update(
                    page_id=page.id, icon={"type": "external", "external": {"url": company_logo_url}}
                )
            # Update Notion Blocks
            page.heading_3(f"Description:")
            for t in company_desc.split('\n'):
                page.paragraph(t)
            page.update()
            print(f"✅ Data successfully updated in Notion.")
```

 
