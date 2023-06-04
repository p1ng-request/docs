<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Enforce_data_types_to_columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Enforce+data+types+to+columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook enforces specific data types to columns using Pandas, elevating your data consistency and accuracy. Availables types:
- Numeric types: int, float, complex
- Textual types: str
- Date and time types: datetime, timedelta
- Categorical types: category
- Boolean type: bool
- Object type: object

**References:**
- [Pandas - DataFrame.astype](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `dtype`: Use a str or a mapping, e.g. {col: dtype, …}, where col is a column label and dtype is a numpy.dtype or Python type to cast one or more of the DataFrame’s columns to column-specific types.


```python
dtype = {
    "team": str,
    "points": int,
    "assists": int,
    "rebounds": float,
}
```

## Model

### Create DataFrame


```python
# create DataFrame
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", "B"],
        "points": [11, 7, '8', 10, 13, 13],
        "assists": [5, 7, 7, 9, 12, 9],
        "rebounds": [11, '8', 10.2, 6.6, 6, 5],
    }
)
df
```


```python
df.info()
```

### Enforce data type to column


```python
df = df.astype(dtype)
df
```

## Output

### Display new types for DataFrame


```python
df.info()
```
