    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Create_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Create+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #productivity #naas_drivers #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** Notion is a powerful tool for creating and organizing digital pages to help you stay organized and productive.

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
