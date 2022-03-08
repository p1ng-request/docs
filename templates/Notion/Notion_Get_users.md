<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Get_users.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook shows how to use Naas Notion driver to get user lists available in your workspace.

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
```

## Model

### Get users


```python
users = notion.connect(token).users.list()
```

## Output


```python
users
```
