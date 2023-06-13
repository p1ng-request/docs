<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Insert_column.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Insert+column:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #column #insert #snippet #operation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook show how to insert column into DataFrame at specified location.

**References:**
- [Pandas - Insert column](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.insert.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `loc`: Insertion index. Must verify 0 <= loc <= len(columns).
- `column`: Label of the inserted column.
- `value`: String, Series, or array-like


```python
loc = 0
column = "championship"
value = "NBA"
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

### Insert column


```python
df.insert(loc=loc, column=column, value=value)
```

## Output

### Display DataFrame


```python
df
```
