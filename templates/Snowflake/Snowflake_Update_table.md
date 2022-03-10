<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Snowflake/Snowflake_Update_table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #snowflake #database #snippet

**Author:** [Sanjay Sabu](https://www.linkedin.com/in/sanjay-sabu-4205/)

## Input

### Import libraries


```python
import csv
from snowflakeconnector import SnowflakeConnector
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
```

## Model

### Read the csv file and converting to list


```python
with open('Excel-Sales_Feb2020.csv') as f:
    reader = csv.reader(f)
    d_list = list(reader)
d_list
```

### Connecting to Snowflake


```python
#Initialize SnowflakeConnector
instance = SnowflakeConnector(username,password,account,database)
```

### Updating Snowflake


```python
for i in range(1,len(d_list)):
    table_insert_csv_query= "INSERT INTO NAAS values"
    table_insert_csv_query = table_insert_csv_query +str(tuple(d_list[i]))
    instance.execute_query(table_insert_csv_query,query_type="push")
```

## Output

### To see contents of table


```python
table_display_query = "select * from " + table_name
#Fetch records from Snowflake database
instance.execute_query(table_display_query,query_type="pull")
```

### Closing the Connection


```python
instance.close_connection()
```

### Display result
