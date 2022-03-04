<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Snowflake - Create table from csv
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Snowflake/Snowflake_Create_table_from_csv.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #snowflake #database

## Input

### Import libraries


```python
import csv
from snowflakeconnector import SnowflakeConnector
import snowflake.connector as snow
import csv
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

### Table Creation 


```python
table_creation = "CREATE TABLE " + table_name + "(MONTH varchar, YEAR int,ITEM varchar,AMOUNT int,CURRENCY varchar)"
cur.execute(table_creation)
```

### Loading the csv


```python
with open('Excel-Sales_Feb2020.csv') as f:
    reader = csv.reader(f)
    d_list = list(reader)
d_list
```

### Inserting into the table


```python
for i in range(1,len(d_list)):
    table_insert_csv_query= "INSERT INTO " + table_name + " VALUES"
    table_insert_csv_query = table_insert_csv_query +str(tuple(d_list[i]))
    instance.execute_query(table_insert_csv_query,query_type="push")
```

## Output

### Showing the updated table


```python
table_display_query = "SELECT * FROM " + table_name
#Fetch records from Snowflake database
instance.execute_query(table_display_query,query_type="pull")
```

### Import library

### Display result
