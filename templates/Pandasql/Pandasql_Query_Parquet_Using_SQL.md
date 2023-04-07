<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandasql/Pandasql_Query_Parquet_Using_SQL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandasql+-+Query+Parquet+Using+SQL:+Error+short+description">Bug report</a>

**Tags:** #pandas #parquet #snippet #read #dataframe #sql #pandasql #operations

**Author:** [Minura Punchihewa](https://www.linkedin.com/in/minurapunchihewa/)

**Description:** This notebook demonstrates how to use Pandasql to query Parquet files as if they were relational databases, using SQL syntax. The aim is to provide an alternative to traditional Pandas methods for filtering, grouping, and aggregating data, and make it easier for users who are familiar with SQL to perform these tasks.

## Input

### Import libraries


```python
import pandas as pd
try:
    from pandasql import sqldf
except:
    !pip install pandasql --user
    from pandasql import sqldf
```

### Setup Variables


```python
# Inputs
file_path = "/home/minura/Documents/data/iris.parquet"
query = """SELECT sepal_length, sepal_width, variety FROM df;"""  # query to be executed
```

## Model

### Read Parquet file into DataFrame


```python
# Read Parquet file into DataFrame
df = pd.read_parquet(file_path)
df
```

### Use sqldf to execute the query


```python
# Use sqldf to execute the query
output_df = sqldf(query)
```

## Output

### Display the resulting DataFrame
The output of the code will be a DataFrame containing only the A column from the original DataFrame df.


```python
output_df
```
