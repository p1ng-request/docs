<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Send_sales_pipeline_to_Notion.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Send+sales+pipeline+to+Notion:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #notion #sales #pipeline #automation #integration

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook automates the process of sending a sales pipeline from HubSpot to Notion. It is useful for organizations that need to keep track of their sales pipeline in both HubSpot and Notion.

**References:**
- [HubSpot API Documentation](https://developers.hubspot.com/docs/overview)
- [Notion API Documentation](https://notion-api.readthedocs.io/en/latest/)

## Input

### Import libraries


```python
import naas
from naas_drivers import hubspot, notion
import pandas as pd
from datetime import datetime
from dateutil.relativedelta import relativedelta
```

### Setup Variables
[Get your HubSpot Access token](https://knowledge.hubspot.com/articles/kcs_article/integrations/how-do-i-get-my-hubspot-api-key)
- `hs_access_token`: This variable stores an access token used for accessing the HubSpot API. It is retrieved from a secret store using naas.secret.get() method. If the access token is not available in the secret store, a default value of "YOUR_HS_ACCESS_TOKEN" is used.
- `pipeline_id`: This variable represents the ID of a pipeline in HubSpot. It is a string value that identifies a specific pipeline within HubSpot's system. To get it you can retrieve your pipelines using this function `hubspot.connect(hs_access_token).pipelines.get_all()`
- `enterprise_id`: This variable stores the ID of an enterprise. It is a string value that represents a unique identifier for an enterprise. You can find it your settings below your "Profile & Preferences".

[Get your Notion token](https://notion-api.readthedocs.io/en/latest/token.html)
- `notion_token`:  This variable stores an access token used for accessing the Notion API. It is retrieved from a secret store using naas.secret.get() method. If the access token is not available in the secret store, a default value of "YOUR_TOKEN" is used.
- `notion_database_key`: This variable represents the key or identifier of a Notion database. It is a string value that uniquely identifies a specific database within Notion.
- `force_update`: This variable is a boolean flag that indicates whether to force an update or not. It is set to False, indicating that an update will not be forced.
- `notion_database`: This variable stores a URL representing a Notion database.


```python
# Inputs
hs_access_token = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
pipeline_id = "0000000"
enterprise_id = "0000000"
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
notion_database_key = "Name"
force_update = False

# Outputs
notion_database = "https://www.notion.so/naas-official/61cf093f0c604eeb8baff67612eb1ac8?v=51965cece44a4cb884a426617f67c88d&pvs=4"
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
    notion_database_key,
    notion_token
)
print("✅ Notion DB:", len(df_notion))
df_notion.head(1)
```

### Get pipelines and dealstages


```python
df_pipelines = hubspot.connect(hs_access_token).pipelines.get_all()
print("✅ Pipelines & dealstages fetched:", len(df_pipelines))
df_pipelines.tail(1)
```

### Get all deals from HubSpot


```python
df_deals = hubspot.connect(hs_access_token).deals.get_all(properties)
print("✅ Deals fetched:", len(df_deals))
df_deals.tail(1)
```

### Prep HubSpot data


```python
def prep_data(
    df_deals,
    df_pipelines,
    pipeline_id=None,
    enterprise_id=None,
):
    # Init
    df = df_deals.copy()
    
    # Reorder columns
    to_order = [
        "pipeline",
        "dealstage",
        "hs_object_id",
        "dealname",
        "createdate",
        "closedate",
        "hs_lastmodifieddate",
        "amount"
    ]
    df = df[to_order]
    
    # Filter on pipeline
    date_limit = (datetime.today() - relativedelta(months=3)).strftime("%Y%m%d%H%M%S")
    df["date_limit"] = pd.to_datetime(df["hs_lastmodifieddate"]).dt.strftime("%Y%m%d%H%M%S")
    df = df[(df["pipeline"] == pipeline_id) & (df["date_limit"].astype(int) > int(date_limit))]
    
    # Add dealstages name and pipeline name
    dealstages = {}
    pipelines = {}
    for index, row in df_pipelines.iterrows():
        pipelines[row["pipeline_id"]] = row["pipeline"]
        dealstages[row["dealstage_id"]] = row["dealstage_label"]

    # Insert names
    df.insert(loc=1, column="pipeline_name", value=df["pipeline"].map(pipelines))
    df.insert(loc=3, column="dealstage_name", value=df["dealstage"].map(dealstages))
    df.insert(loc=0, column="deal_link", value=f"https://app.hubspot.com/contacts/{enterprise_id}/deal/" + df["hs_object_id"])
    
    # Prep data
    for col in df.columns:
        if 'date' in col:
            df[col] = df[col].str[:19].str.replace("T", " ")
    df["amount"] = df["amount"].fillna(0)
    return df.reset_index(drop=True)

df_hubspot = prep_data(df_deals, df_pipelines, pipeline_id, enterprise_id)
print("✅ HubSpot data:", len(df_hubspot))
df_hubspot.tail(5)
```

### Get rows to update
If `force_update` is set to `True`, the entire database will be updated.<br>


```python
def get_new_rows(
    df_hubspot,
    df_notion,
    force_update,
):
    # Check if df_hubspot is not empty
    if len(df_hubspot) == 0:
        return pd.DataFrame()
    
    # Check if df is not empty
    if len(df_notion) == 0:
        return df_hubspot
    
    # Return all rows if force update is True
    if force_update:
        return df_hubspot.reset_index(drop=True)
    
    # Update page ID
    pages = {}
    last_update_dates = {}
    for index, row in df_notion.iterrows():
        deal_id = row["Deal ID"]
        last_update = row["Last modified date"]
        page_id = row["PAGE_ID"]
        pages[deal_id] = page_id
        last_update_dates[deal_id] = last_update
        
    df_hubspot["Last modified date"] = df_hubspot["hs_object_id"].map(last_update_dates).fillna(0)
    df_hubspot["PAGE_ID"] = df_hubspot["hs_object_id"].map(pages).fillna(0)
    
    # Filter on date
    df_hubspot["date_init"] = pd.to_datetime(df_hubspot["Last modified date"]).dt.strftime("%Y%m%d%H%M")
    df_hubspot["date_new"] = pd.to_datetime(df_hubspot["hs_lastmodifieddate"]).dt.strftime("%Y%m%d%H%M")
    df_hubspot = df_hubspot[df_hubspot["date_init"] != df_hubspot["date_new"]]
    return df_hubspot.reset_index(drop=True)

df_new_rows = get_new_rows(
    df_hubspot,
    df_notion,
    force_update
)
print("Rows to update:", len(df_new_rows))
df_new_rows.head(len(df_new_rows))
```

## Output

### Update Notion database


```python
database_id = notion_database.split("/")[-1].split("?v=")[0]
if len(df_new_rows) > 0:
    # Loop to enrich info
    for index, row in df_new_rows.iterrows():
        # Init variables
        name = row["dealname"]
        page_id = row["PAGE_ID"]
        print("➡️ Update info for:", name)

        # Get page
        try:
            if page_id == 0:
                page = notion.connect(notion_token).Page.new(database_id=database_id).create()
                page.title("Name", name)
                page.update()
            else:
                page = notion.connect(notion_token).page.get(page_id)

            # Update Notion
            page.title("Name", name)
            page.link("HubSpot link", row['deal_link'])
            page.rich_text("Deal ID", row['hs_object_id'])
            page.rich_text("Pipeline ID", row["pipeline"])
            page.select("Pipeline name", row["pipeline_name"])
            page.rich_text("Dealstage ID", row["dealstage"])
            page.select("Dealstage name", row["dealstage_name"])
            page.number("Amount", float(row["amount"]))
            page.date("Created date", row["createdate"])
            page.date("Last modified date", row["hs_lastmodifieddate"])
            if str(row["closedate"]) != "None":
                page.date("Close date", row["closedate"])
            page.update()   
            print(f"✅ Data successfully updated in Notion.")
        except Exception as e:
            print(e)
            print(row)
```


```python

```
