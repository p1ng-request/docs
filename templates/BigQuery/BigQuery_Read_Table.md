    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/BigQuery/BigQuery_Read_Table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=BigQuery+-+Read+Table:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bigquery #database #snippet #operations #dataframe

**Author:** [Minura Punchihewa](https://www.linkedin.com/in/minurapunchihewa/)

**Description:** This notebook provides an example of how to read data from a BigQuery table.

## Input

### Import libraries


```python
from naas_drivers import bigquery
```

### Variable


```python
service_account_file = "big-query-777777-ffffff777777.json"
project_id = "big-query-777777"
dataset = "example_ds"
table_name = "iris"
```

## Model

### Connect to BigQuery


```python
conn = bigquery.connect(service_account_file, project_id)
```

## Output

### Read the table


```python
df = conn.execute_query(f"SELECT * FROM {dataset}.{table_name}")
```


```python
df
```
