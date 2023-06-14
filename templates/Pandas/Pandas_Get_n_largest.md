<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Get_n_largest.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Get+n+largest:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #nlargest #python #data #analysis

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will demonstrate how to use the `nlargest` function in Pandas to get the n largest values from a DataFrame. This is useful for data analysis and data manipulation.

**References:**
- [Pandas Documentation - nlargest](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.nlargest.html)
- [Stack Overflow - nlargest](https://stackoverflow.com/questions/15741759/find-maximum-value-of-a-column-and-return-the-corresponding-row-values-using-pan)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables

- `n`: Number of items to retrieve.
- `column`: Column name or names to order by.


```python
n = 2
column = "Age"
```

## Model

### Create dataframe


```python
# Create a fake dataset
data = {"Name": ["Tom", "nick", "krish", "jack"], "Age": [20, 21, 19, 18]}
# Create a DataFrame
df = pd.DataFrame(data)
```

## Output

### Get n largest

The `nlargest` function can be used to get the n largest values from a DataFrame. The two largest values are displayed below.


```python
# D
df.nlargest(n, column)
```

 
