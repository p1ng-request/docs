<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Airtable/Airtable_Connect.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #airtable #database #productivity #spreadsheet #naas_drivers

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

## Input

### Import library


```python
from naas_drivers import airtable
```

### Variables


```python
API_KEY = 'API_KEY'
BASE_KEY = 'BASE_KEY'
TABLE_NAME = 'TABLE_NAME'
```

## Model

### Connect to airtable


```python
AT = airtable.connect(API_KEY, BASE_KEY, TABLE_NAME)
```

## Output

### Display result


```python
AT
```
