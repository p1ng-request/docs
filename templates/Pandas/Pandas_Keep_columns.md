<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Keep_columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Keep+columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to define a new DataFrame that only keeps columns defined in Input section.

**References:**
- [Pandas - Keep columns](https://www.statology.org/pandas-keep-columns/)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `to_keep`: list of columns to keep in dataframe


```python
to_keep = ["team", "points", "blocks"]
```

## Model

### Create DataFrame


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

### Create new DataFrame that only keeps defined columns
You can't set one column that does not exists in your dataframe so we managed it in the function below.


```python
def keep_columns(df, to_keep):
    # Check if all columns exist in dataframe
    for i, x in enumerate(to_keep):
        if not x in df.columns:
            print(
                f"🚨 Columns '{x}' does not exist in DataFrame -> removed from your list!"
            )
            to_keep.pop(i)
    df1 = df[to_keep]
    return df1
```

## Output

### Display new DataFrame


```python
df1 = keep_columns(df, to_keep)
df1
```
