    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Create_pages_in_database_from_dataframe.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Create+pages+in+database+from+dataframe:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #database #dataframe #python #create #pages

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create pages in Notion database from a dataframe. It could be very usefull to kick start a new database in Notion with historical data stored in CSV, Excel or Google Sheets.

**References:**
- [Notion Drivers Naas](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/notion.py)
- [Notion API Documentation](https://developers.notion.com/)

## Input

### Import libraries


```python
import naas
import pandas as pd
from naas_drivers import notion
```

### Setup Variables
- `notion_token`: Get your [Notion integration token](https://docs.naas.ai/drivers/notion) and share it with your database
- `df`: DataFrame as example.
- `df_key_name`: DataFrame column name to used as key
- `notion_key_name`: Notion column name to used as key
- `notion_database`: Notion Database URL


```python
# Inputs
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_NOTION_TOKEN"
notion_key_name = "Customer"
df = pd.DataFrame({"CUSTOMER": ["Customer 1", "Customer 2", "Customer 3"]})
df_key_name = "CUSTOMER"

# Outputs
notion_database = "https://www.notion.so/asgard-group/bba2fd39a1ed457ba8e90a1104e58d13?v=39b4ecexxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

## Model

### Get dataframe


```python
print("✅ Dataframe init:", len(df))
df.head(3)
```

## Output

### Create pages in Notion database
If page already exists, a new page won't be created.


```python
def create_pages(
    notion_token,
    notion_database,
    notion_key_name,
    df,
    df_key_name,
):
    # Get pages
    database_id = notion_database.split("/")[-1].split("?v=")[0]
    pages = notion.connect(notion_token).database.query(database_id, query={})
    
    # Manage dataframe empty
    if len(df) == 0:
        print("🛑 Nothing to update in Notion.")
        return
    
    # Loop in data 
    for i, row in df.iterrows():
        df_key = row[df_key_name]
        print(f"➡️ {i} - Started with '{df_key}'")
        
        # Create or update page
        page_new = True
        for page in pages:
            page_temp = page.df()
            page_id = page_temp.loc[page_temp.Name == notion_key_name, "Value"].values
            if page_id == df_key:
                page_new = False
                print(f"❎ Page already exists in Notion")
                break
        try:
            if page_new:
                # Create new page in notion
                page = notion.connect(notion_token).Page.new(database_id=database_id).create()
                page.title(notion_key_name, df_key)
                
                # You
                page.update()
                print(f"✅ Page created in Notion.", '\n')
        except Exception as e:
            print(f"❌ Error creating page in Notion", e)
            print(row)
            
create_pages(
    notion_token,
    notion_database,
    notion_key_name,
    df,
    df_key_name,
)
```
