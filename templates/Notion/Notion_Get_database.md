<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Get_database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Get+database:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #productivity #naas_drivers #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** Notion is a powerful database tool that helps you organize and store your data in an intuitive and efficient way.

## Input

### Import library


```python
from naas_drivers import notion
```

### Setup Notion
<a href='https://docs.naas.ai/drivers/notion'>How to get your Notion integration token ?</a>


```python
# Enter Token API
token = "*****"

# Enter Database URL
database_url = "https://www.notion.so/********"
```

## Model

### Get database from Notion


```python
database = notion.connect(notion_token).database.get(database_url, query={})
```

## Output

### Database object


```python
database
```

### Dataframe


```python
df_notion = database.df()
df_notion
```
