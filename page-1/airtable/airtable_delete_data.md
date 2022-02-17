# Airtable\_delete\_data

![Naas](https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160)

## Airtable - Delete data

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/open\_in\_naas.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Airtable/Airtable\_delete\_data.ipynb)

**Tags:** #airtable #database #productivity #spreadsheet #naas\_drivers

### Input

#### Import library

```python
from naas_drivers import airtable
```

#### Variables

```python
API_KEY = 'API_KEY'
BASE_KEY = 'BASE_KEY'
TABLE_NAME = 'TABLE_NAME'
```

### Model

#### Delete data

```python
at = airtable.connect(API_KEY, BASE_KEY, TABLE_NAME).delete_by_field('Name', 'Tom')
```

### Output

#### Display result

```python
at
```
