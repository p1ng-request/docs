<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Drop_duplicates.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Drop+duplicates:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Sunny Chugh](https://www.linkedin.com/in/sunny-chugh-ab1630177/)

**Description:** This notebook shows how to drop duplicates in a DataFrame.

**References:**
- [Pandas - Drop duplicates](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html)
- https://www.statology.org/pandas-drop-duplicate-columns/

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `subset`: column label or sequence of labels. Only consider certain columns for identifying duplicates, by default use all of the columns.
- `keep`: {‘first’, ‘last’, False}, default ‘first’. Determines which duplicates (if any) to keep: ‘first’ : Drop duplicates except for the first occurrence; ‘last’ : Drop duplicates except for the last occurrence; False : Drop all duplicates.


```python
subset = None
keep = "first"
```

## Model

### Create DataFrame


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
print("Columns fetched:", len(df.columns))
print("Rows fetched:", len(df))
df
```

## Output

### Drop Duplicated rows


```python
df1 = df.drop_duplicates(subset, keep=keep, ignore_index=True)
print("Rows fetched:", len(df1))
df1
```

### Drop Duplicated columns even if column names are different


```python
df2 = df.T.drop_duplicates().T
print("Columns fetched:", len(df2.columns))
df2
```
