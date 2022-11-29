<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Rename_Columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Rename+Columns:+Error+short+description">Bug report</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook renames columns in a dataframe.

## Input

### Import libraries


```python
import pandas as pd
```

### Setup DataFrame


```python
#create DataFrame
df = pd.DataFrame({'team': ['A', 'A', 'A', 'B', 'B', 'B'],
                   'points': [11, 7, 8, 10, 21, 13],
                   'assists': [5, 7, 7, 9, 12, 0],
                   'rebounds': [5, 8, 10, 6, 6, 22]})
df
```

### Define columns to rename
This function will not throw an error if column does not exist in dataframe.


```python
# dict of columns with new names
to_rename = {
    'team': "equipo",
    'points': "puntos",
    'assists': "asistancias",
    'rebounds': "rebotes",
    "col": "new_col"
}
```

## Model

### Rename columns in dataframe


```python
df = df.rename(columns=to_rename)
```

## Output

### View new DataFrame


```python
df
```
