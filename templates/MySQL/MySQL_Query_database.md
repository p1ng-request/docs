<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/MySQL/MySQL_Query_database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #mysql #database

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

## Input

### Import libraries


```python
import os
import pymysql
import pandas as pd
```

### Variables


```python
host = os.getenv('MYSQL_HOST')
port = os.getenv('MYSQL_PORT')
user = os.getenv('MYSQL_USER')
password = os.getenv('MYSQL_PASSWORD')
database = os.getenv('MYSQL_DATABASE')
```

## Model

### Connect to database


```python
conn = pymysql.connect(
    host=host,
    port=int(port),
    user=user,
    passwd=password,
    db=database,
    charset='utf8mb4')
```

### Send the query


```python
df = pd.read_sql_query(
    "SELECT DATE(created_at) AS date, COUNT(*) AS count FROM user GROUP BY date HAVING date >= '2017-04-01' ",
    conn)
df.tail(10)
```

## Output

### Display result


```python
%matplotlib inline

df.index = df['date']
p = df.tail(10).plot.bar()
```


```python
conn.close()
```
