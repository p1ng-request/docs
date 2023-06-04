<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Rename_columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Rename+columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook renames columns in a dataframe.

**References:**
- [Pandas - Rename Columns](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `to_rename`: dict of columns with new names


```python
to_rename = {
    "team": "equipo",
    "points": "puntos",
    "assists": "asistancias",
    "rebounds": "rebotes",
    "col": "new_col",
}
```

## Model

### Create dataframe


```python
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", "B"],
        "points": [11, 7, 8, 10, 21, 13],
        "assists": [5, 7, 7, 9, 12, 0],
        "rebounds": [5, 8, 10, 6, 6, 22],
    }
)
df
```

### Rename columns in dataframe


```python
df = df.rename(columns=to_rename)
```

## Output

### Display new DataFrame


```python
df
```


```python

```
