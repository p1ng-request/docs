<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Drop_Columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Drop+Columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to define a new DataFrame that drops columns defined in Input section.

<u>Reference:</u> https://www.statology.org/pandas-keep-columns/

## Input

### Import libraries


```python
import pandas as pd
```

### Setup DataFrame


```python
# create DataFrame
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", "B"],
        "points": [11, 7, 8, 10, 13, 13],
        "assists": [5, 7, 7, 9, 12, 9],
        "rebounds": [11, 8, 10, 6, 6, 5],
    }
)
df
```

### Define columns to drop


```python
# list of columns to drop in dataframe
to_drop = ["team", "points", "blocks"]
```

## Model

### Create new DataFrame that drops defined columns
Only columns that exist in DataFrame will be droped with the function below.


```python
def drop_columns(df, to_drop):
    # Check if all columns exist in dataframe
    for c in to_drop:
        if c in df.columns:
            df[c] = df.drop(c, axis=1)
    else:
        print(f"🚨 Columns '{c}' does not exist in DataFrame!")
    return df
```

## Output

### View new DataFrame


```python
df1 = drop_columns(df, to_drop)
df1
```
