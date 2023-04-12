<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Airtable/Airtable_Get_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Airtable+-+Get+data:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #airtable #database #productivity #spreadsheet #naas_drivers #operations #snippet #dataframe

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook provides an introduction to Airtable, a cloud-based database platform that allows users to easily access and manage data. It provides step-by-step instructions on how to get data from Airtable into a notebook for further analysis.

## Input

### Import library


```python
from naas_drivers import airtable
```

### Variables


```python
API_KEY = "API_KEY"
BASE_KEY = "BASE_KEY"
TABLE_NAME = "TABLE_NAME"
```

## Model

### Connect to airtable and get data


```python
df = airtable.connect(API_KEY, BASE_KEY, TABLE_NAME).get(
    view="All opportunities", maxRecords=20
)
```

## Output

### Display result


```python
df
```
