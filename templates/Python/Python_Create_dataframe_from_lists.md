<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Create_dataframe_from_lists.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Create+dataframe+from+lists:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #list #dataframe #snippet #pandas #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides instructions on how to use Python to create a dataframe from lists.

## Input

### Import libraries


```python
import pandas as pd
```

### Variables


```python
# Setup your columns name
col_key = "KEYS"
col_value = "VALUE"
```

### Lists


```python
keys = [
    1995,
    1996,
    1997,
    1998,
    1999,
    2000,
    2001,
    2002,
    2003,
    2004,
    2005,
    2006,
    2007,
    2008,
    2009,
    2010,
    2011,
    2012,
]
value = [
    219,
    146,
    112,
    127,
    124,
    180,
    236,
    207,
    236,
    263,
    350,
    430,
    474,
    526,
    488,
    537,
    500,
    439,
]
```

## Model

### Create zip iterator


```python
# Call zip(iter1, iter2) with one list as iter1 and another list as iter2 to create a zip iterator containing pairs of elements from the two lists.
zip_iterators = zip(keys, value)
```

## Output

### Create dataframe


```python
df = pd.DataFrame(zip_iterators, columns=[col_key, col_value])
df
```


```python

```
