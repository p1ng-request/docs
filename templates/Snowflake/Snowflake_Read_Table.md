<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Snowflake/Snowflake_Read_Table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #snowflake #database #snippet

**Author:** [Sanjay Sabu](https://www.linkedin.com/in/sanjay-sabu-4205/)

## Input

### Import libraries


```python
import pandas as pd
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
table_name = "NAAS"
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

### To see contents of table


```python
table_display_query = "select * from " + table_name
#Fetch records from Snowflake database
instance.execute_query(table_display_query,query_type="pull")
```

### Reading data from the table


```python
data = instance.execute_query(table_display_query,query_type="pull")
```

## Output

### Fetching table details


```python
table_description_query = "DESCRIBE " + table_name
table_details = instance.execute_query(table_description_query,query_type="pull")
header = table_details[0]
```

### Preparing csv file


```python
data = pd.DataFrame(data)
data.columns=[header]
data.to_csv('naas_output.csv')
data
```

### Import library

### Display result
