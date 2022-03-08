<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Create_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook shows how to use Naas Notion driver to create a page inside a database

**Tags:** #notion #productivity

## Input

### Import libraries


```python
from naas_drivers import notion 
```

### Input variables
<a href='https://docs.naas.ai/drivers/notion'>How to get your Notion integration token ?</a>


```python
# Enter Token API
token = "*****"

# Enter Database URL
database_id = "https://www.notion.so/naas-official/fafef5183c42474987e002d30ba55d18?v=814c0ec7f34a4395aba47c4eeced603f"
```

## Model


```python
page = notion.connect(token).page.create(database_id=database_id, title="My new page")
```

## Output


```python
page
```
