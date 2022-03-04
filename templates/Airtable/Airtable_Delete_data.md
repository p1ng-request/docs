<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Airtable - Delete data
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Airtable/Airtable_Delete_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

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

### Delete data


```python
data = airtable.connect(API_KEY,
                        BASE_KEY,
                        TABLE_NAME).delete_by_field('Name', 'Tom')
```

## Output

### Display result


```python
data
```
