<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Drop_Duplicate_Columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Drop+Duplicate+Columns:+Error+short+description">Bug report</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Sunny Chugh](https://www.linkedin.com/in/sunny-chugh-ab1630177/)

**Description:** This notebook shows how to define a new DataFrame that drops duplicate columns in the dataframe

<u>Reference:</u> https://www.statology.org/pandas-drop-duplicate-columns/

## Input

### Import libraries


```python
import pandas as pd
```

### Setup DataFrame


```python
# create DataFrame with duplicate columns
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "A", "B", "B", "B", "B"],
        "points1": [25, 25, 15, 14, 19, 23, 25, 29],
        "points2": [25, 25, 15, 14, 19, 23, 25, 29],
        "rebounds": [11, 11, 10, 6, 6, 5, 9, 12],
    }
)

# view DataFrame
df
```

## Model

### Drop Duplicate columns with subset
subset : column label or sequence of labels, optional
Only consider certain columns for identifying duplicates, by default use all of the columns.


```python
subset = ["team"]


def drop_columns(df, subset=None):
    return df.drop_duplicates(subset)


df1 = drop_columns(df, subset)
df1
```

### Drop Duplicate columns even if column names are different


```python
def drop_columns(df):
    return df.T.drop_duplicates().T


df2 = drop_columns(df)
df2
```

## Output

### View new DataFrame


```python
df1
```

### View new DataFrame


```python
df2
```
