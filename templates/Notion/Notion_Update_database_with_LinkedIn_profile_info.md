<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Update_database_with_LinkedIn_profile_info.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Update+database+with+LinkedIn+profile+info:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #database #update #linkedin #company #automation #scheduler

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook streamlines the process of updating a Notion database containing profile names by extracting relevant information from LinkedIn using Google search, as well as utilizing Naas_Drivers.Notion and Naas_Drivers.LinkedIn. The following data will be updated in your Notion database:
- Name: The name of the person who owns the LinkedIn profile.
- LinkedIn: LinkedIn unique URL
- Occupation: The job or profession that a person is engaged in, listed on their LinkedIn profile.
- Industry: The field or sector in which a person works, listed on their LinkedIn profile.
- City: The specific city where a person lives or works, listed on their LinkedIn profile.
- Region: A broader geographic area that a person's city may be located in, such as a state or province, listed on their LinkedIn profile.
- Country: The nation where a person is located or from, listed on their LinkedIn profile.
- Location: The overall geographic location of a person, which may include their city, region, and country, listed on their LinkedIn profile.
Additionally, the background picture will be refreshed as the page cover, the profile picture will serve as the page icon, and the occupation and summary will be included in the page block.

Overall, this notebook can be useful for any business or individual who needs to keep track of company information for various purposes:
- Lead generation: Sales teams could use the updated Notion database to identify potential leads based on their LinkedIn profiles, and initiate targeted outreach to convert them into customers.
- Talent sourcing: Recruiters could use the updated Notion database to find and evaluate potential job candidates based on their LinkedIn profiles and relevant information stored in the database.
- Social media marketing: Marketers could use the updated Notion database to build custom audiences for their social media campaigns based on the information stored in the database and on LinkedIn.

<u>Disclamer:</u>

When using this script to scrape profiles from LinkedIn, it's important to set a limit on the number of API calls made to avoid being temporarily banned. LinkedIn heavily monitors scraping activities, and excessive usage can result in a ban. We recommend setting a limit of no more than 5 calls per hour to minimize the risk of being banned. As the owner of the script, it's your responsibility to use it responsibly and abide by LinkedIn's terms of service. We assume no liability for any consequences resulting from your use of this script.

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
- `limit`: Specify the maximum number of profiles to be scraped during each execution.

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
limit = 5 
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
database_key = "Name"
database_linkedin = "LinkedIn"
force_update = False

# Outputs
notion_database = "https://www.notion.so/xxxxxxxxxxxx"
output_dir = "profiles"
```

### Schedule your automation


```python
# Schedule during week days every hour between 9:00 AM to 8:00 PM
naas.scheduler.add(cron="0 9-20 * * 1-5")

# naas.scheduler.delete() # uncomment and execute cell to delete automation
```

## Model

### Constants
- `LINKEDIN_PATTERN`: LinkedIn profile pattern to be searched in Google


```python
LINKEDIN_PATTERN = "https:\/\/.+.linkedin.com\/in\/*([^?])+"
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
        return df.reset_index(drop=True)
    
    # Check if LinkedIn col exists in df to filter rows
    if linkedin_col in df.columns:
        # Get LinkedIn IR
        df["LINKEDIN_ID"] = df.apply(lambda row: row[linkedin_col].split("/in/")[-1].split("/")[0], axis=1)
        
        # Get list of valid URL
        linkedin_valid = df[
            (df[linkedin_col].str.match(LINKEDIN_PATTERN)) & 
            (df["LINKEDIN_ID"].str[:5] == "ACoAA")
        ][linkedin_col].unique()
        df = df[~df[linkedin_col].isin(linkedin_valid)]
    else:
        df[linkedin_col] = None
    return df.reset_index(drop=True)

df_new_rows = get_new_rows(df_notion, database_linkedin, force_update)
print("Rows to update:", len(df_new_rows))
df_new_rows.head(len(df_new_rows))
```

### Get rows to update


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
    url = "https://www.linkedin.com/in/ACoAA"
    
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
    limit,
):
    # Limit df
    df = df[:limit]

    # Check if df is not empty
    if len(df) == 0:
        return pd.DataFrame()
    else:
        df[linkedin_col] = df.apply(lambda row: get_linkedin_url(row, key, linkedin_col), axis=1)
        return df.reset_index(drop=True)[:limit]

df_update = udpate_linkedin_url(
    df_new_rows,
    database_key,
    database_linkedin,
    limit,
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
        lk_public_id = lk_url.split("/in/")[-1].split("/")[0]
        page_id = row["PAGE_ID"]
        print("➡️ Update info for:", name)

        # Get page
        page = notion.connect(notion_token).page.get(page_id)
        
        # Get LinkedIn Info
        if lk_public_id != "ACoAA":
            df = linkedin.connect(li_at, JSESSIONID).profile.get_identity(lk_url)
            df = df.astype(str).replace("None", "")
            lk_id = df.loc[0, "PROFILE_ID"]
            lk_url = df.loc[0, "PROFILE_URL"]
            firstname = df.loc[0, "FIRSTNAME"]
            lastname = df.loc[0, "LASTNAME"]
            fullname = f"{firstname} {lastname}"
            summary = df.loc[0, "SUMMARY"]
            industry = df.loc[0, "INDUSTRY_NAME"]
            occupation = df.loc[0, "OCCUPATION"]
            country = df.loc[0, "COUNTRY"]
            region = df.loc[0, "REGION"]
            location = df.loc[0, "LOCATION"]
            profile_picture = df.loc[0, "PROFILE_PICTURE"]
            bg_picture = df.loc[0, "BACKGROUND_PICTURE"]

            # Save dataframe
            fullname_c = fullname.replace(' ', '_')
            csv_name = f"{datetime.now().strftime('%Y%m%d%H%M%S')}_LINKEDIN_IDENTITY_{lk_id}.csv"
            output_path = os.path.join(output_dir, fullname_c)
            if not os.path.exists(output_path):
                os.makedirs(output_path)
            csv_path = os.path.join(output_path, csv_name)
            df.to_csv(csv_path, index=False)
            print(f"✅ Data saved to csv:", csv_path)

            # Update Notion
            page.title("Name", fullname)
            page.link(database_linkedin, lk_url)
            page.rich_text("Occupation", occupation)
            page.rich_text("Region", region)
            if industry != "":
                page.select("Industry", industry)
            if country != "":
                page.select("Country", country)
            if location != "":
                page.select("Location", location)
            page.update()   
            print(f"✅ Data successfully updated in Notion.")
            
            # Update Image in page
            if str(profile_picture) != "None" and profile_picture.startswith("https://media"):
                notion.client.pages.update(
                    page_id=page.id, icon={"type": "external", "external": {"url": profile_picture}}
                )
                print(f"✅ Picture successfully updated in Notion.")
            if str(bg_picture) != "None" and bg_picture.startswith("https://media"):
                notion.client.pages.update(
                    page_id=page.id, cover={"type": "external", "external": {"url": bg_picture}}
                )
                print(f"✅ Background successfully updated in Notion.")
                
            # Update page blocks
            page.heading_2("Profile")
            page.heading_3("Summary")
            for t in summary.split('\n'):
                page.paragraph(t)
            page.update()
            print(f"✅ Summary successfully updated in Notion.")
            
            # Sleep time
            time.sleep(5)
        else:
            page.link(database_linkedin, lk_url)
            page.update()
            print(f"✅ LinkedIn URL to be updated.")
```

 
