<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Get_n_smallest.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Get+n+smallest:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #nsmallest #python #data #analysis

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook explains how to use the `nsmallest` function from the Pandas library to get the n smallest values from column in a DataFrame.

**References:**
- [Pandas Documentation - nsmallest](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.nsmallest.html)
- [Stack Overflow - nsmallest](https://stackoverflow.com/questions/50995090/pandas-dataframe-nsmallest-function)

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
data = {
    "Name": ["Tom", "nick", "krish", "jack"],
    "Age": [20, 21, 19, 18]
}

# Create a DataFrame
df = pd.DataFrame(data)
df
```

## Output

### Get n smallest values
The `nsmallest` function from the Pandas library allows to get the n smallest values from a DataFrame.


```python
# Display the result
df.nsmallest(n, column)
```

 
