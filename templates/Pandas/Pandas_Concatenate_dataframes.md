<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Concatenate_dataframes.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Concatenate+dataframes:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #concatenate #dataframe #snippet #operations

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook demonstrates how to concatenate dataframes across rows or columns using the Pandas library.

**References:**
- [Pandas - concat](https://pandas.pydata.org/docs/reference/api/pandas.concat.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `df1`: DataFrame object
- `df2`: DataFrame object
- `axis`: The axis to concatenate along. 0 ="index", 1 ="columns"


```python
df1 = pd.DataFrame({'A': [1, 2, 3, 4], 'B': [4, 5, 6, 7]})
df2 = pd.DataFrame({'A': [7, 8, 9], 'B': [10, 11, 12]})
axis = 0
```

## Model

### Display DataFrame 1


```python
print("Columns fetched:", len(df1.columns))
print("Rows fetched:", len(df1))
df1
```

### Display DataFrame 1


```python
print("Columns fetched:", len(df2.columns))
print("Rows fetched:", len(df2))
df2
```

## Output

### Concatenate dataframes


```python
df_concat = pd.concat([df1, df2], axis=axis).reset_index(drop=True)
print("Columns fetched:", len(df_concat.columns))
print("Row fetched:", len(df_concat))
df_concat
```


```python

```
