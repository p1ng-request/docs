<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Snowflake/Snowflake_Delete_table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #snowflake #database

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

## Input

### Import library


```python
from snowflakeconnector import SnowflakeConnector
import snowflake.connector as snow
```

### Insert your credentials


```python
username = "sanjaynaas"
password = "Password123"
```

### Specify your account details


```python
account = "iz84541.europe-west4.gcp"
database = "DEMO_DB"
table_name = "NAAS_NEW"
warehouse_name = "COMPUTE_WH"
schema_name = "PUBLIC"
```

## Model

### Connecting to Snowflake


```python
conn = snow.connect(user=username,password=password,account=account)
cur = conn.cursor()
instance = SnowflakeConnector(username,password,account,database)
```

### Setting the environment


```python
admin = "USE ROLE SYSADMIN"
cur.execute(admin)
warehouse_selection = "USE WAREHOUSE " + warehouse_name
cur.execute(warehouse_selection)
database_selection = "USE DATABASE " + database
cur.execute(database_selection)
schema_selection = "USE SCHEMA " + schema_name
cur.execute(schema_selection)
```

### To see existing tables 


```python
instance.execute_query("show tables",query_type="pull")
```

## Output

### Table deletion


```python
table_deletion = "DROP TABLE " + table_name 
cur.execute(table_deletion)
```

### Table list after deletion


```python
table_display_query = "SHOW TABLES" 
#Fetch records from Snowflake database
instance.execute_query(table_display_query,query_type="pull")
```

### Display result
