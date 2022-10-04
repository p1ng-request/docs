<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PostgresSQL/PostgresSQL_Get_data_from_database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #postgressql #database #operations #snippet #dataframe

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

## Input

### Import librairies


```python
try:
    import psycopg2
except:
    !pip install psycopg2-binary --user
    import psycopg2
import pandas as pd
import naas
```

### Setup PostgresSQL


```python
# Credentials
PG_USER = "YOUR_PG_USER"
PG_PASSWORD = "YOUR_PG_PASSWORD"
PG_HOST = "YOUR_PG_HOST"
PG_DBNAME = "YOUR_PG_DBNAME"

# Database
DATABASE = "YOUR_DATABASE"
SELECTED_FIELD = "*" # "*" or list of columns

# SQL Requests
SQL_REQUEST = f"SELECT {SELECTED_FIELD} FROM {DATABASE}"
```

## Model

### Connect to PostgresSQL


```python
PG = psycopg2.connect(f"user={PG_USER} password={PG_PASSWORD} dbname={PG_DBNAME} host={PG_HOST}")
```

### Get naas users


```python
def get_data():
    cur = PG.cursor()
    cur.execute(SQL_REQUEST)
    res = cur.fetchall()
    cur.close()
    df = pd.DataFrame(res)
    return df

df = get_data()
```

## Output

### Display result


```python
df
```
