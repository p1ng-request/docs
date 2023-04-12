    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Delete_all_pages_from_database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Delete+all+pages+from+database:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #productivity #naas_drivers #operations #snippet #database

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook deletes all page from a Notion database.

## Input

### Import libraries


```python
from naas_drivers import notion
```

### Setup Notion
- [Get your Notion integration token](https://docs.naas.ai/drivers/notion)
- Share integration with your database


```python
# Enter Token API
NOTION_TOKEN = "ENTER_YOUR_NOTION_TOKEN_HERE"  # EXAMPLE: "secret_xxxxxxxxxxxxxxxxxx"

# Enter Page URL
DATABASE_URL = "ENTER_YOUR_DATABASE_URL_HERE"  # EXAMPLE: "https://www.notion.so/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

## Model

### Get page


```python
def delete_all_pages(database_url, token):
    # Get pages
    database_id = database_url.split("/")[-1].split("?v=")[0]
    pages = notion.connect(token).database.query(database_id, query={})
    for page in pages:
        notion.connect(token).blocks.delete(page.id)
        print(f"{page.id} removed from database")
```

## Output

### Delete all pages from database


```python
delete_all_pages(DATABASE_URL, NOTION_TOKEN)
```
