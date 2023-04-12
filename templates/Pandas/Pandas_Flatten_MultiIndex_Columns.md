    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Flatten_MultiIndex_Columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Flatten+MultiIndex+Columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #multiindex #flatten #columns

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to flatten a MultiIndex column in a Pandas DataFrame.

**References:**
- [SparkByExamples.com - Pandas MultiIndex DataFrame Examples](https://sparkbyexamples.com/pandas/pandas-multiindex-dataframe-examples/)
- [Pandas Documentation - MultiIndex / Advanced Indexing](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables


```python
# Inputs
url = "https://en.wikipedia.org/wiki/List_of_cities_by_population"
```

## Model

### Read dataframe with MultiIndex Columns


```python
df = pd.read_html(url)[1]
df.head(3)
```

## Output

### Flatten MultiIndex Columns


```python
# Flatten the columns of the DataFrame
df.columns = df.columns.get_level_values(1)
df
```

 
