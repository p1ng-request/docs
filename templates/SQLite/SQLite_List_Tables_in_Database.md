<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/SQLite/SQLite_List_Tables_in_Database.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=SQLite+-+List+Tables+in+Database:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #SQLite #database #databasemanagement #filebaseddb #dbcreation #dbsetup #SQLiteDB #localstorage #datastore #SQLitedatabase #embeddedDB #PythonDB #sqllite3 #DBfile

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook lists tables within a SQLite database.

**About SQLlite ?**

SQLite is a lightweight, file-based database management system that can be embedded into other applications to provide local data storage. Because of its small footprint, it is often used as an embedded database in mobile and desktop applications, as well as in web browsers and other programs that need a local data storage option.

Here are a few reasons why SQLite can be useful for working with data:

Easy to use and integrate: SQLite is written in C and provides a simple, easy-to-use API for working with databases. The SQLite library is lightweight and can be easily integrated into other applications without the need for additional dependencies or software.

- Serverless: Unlike other databases like MySQL and PostgreSQL, SQLite does not require a separate server process to be running in order to work. Instead, it reads and writes directly to a database file on disk, which makes it easy to set up and use in a variety of environments.

- Cross-platform: SQLite is available for a wide range of platforms, including Windows, macOS, Linux, iOS, and Android. This means that you can develop and deploy applications that use SQLite on multiple platforms with minimal changes.

- Scalable: SQLite is capable of handling large amounts of data, with the maximum size of a database file limited by the amount of free disk space available. The database can handle many concurrent connections and read-write accesses.

- ACID compliant: SQLite follows the ACID properties (Atomicity, Consistency, Isolation, Durability) which means that once you perform any transaction it will be guaranteed to be completed successfully or not at all. This makes it a good fit for mission critical systems, as it is reliable.

- Open Source: SQLite is open-source software, which means that it is free to use and distribute. It also means that developers can access the source code, which can be useful for understanding how the database works and for troubleshooting problems.

Overall, SQLite is a very powerful, reliable and fast database. Its small footprint and ease of integration make it a great option for a wide variety of applications that require local data storage.

## Input

### Import libraries


```python
import sqlite3
```

### Setup Variables


```python
# database name
db_name = "mydatabase.db"
```

## Model

### Create tables in database
Init script to be able to list them next.


```python
# Connect to the database (or create it if it doesn't exist)
conn = sqlite3.connect(db_name)
c = conn.cursor()

# Create tables
c.execute(
    """CREATE TABLE IF NOT EXISTS employees
             (id INTEGER PRIMARY KEY, name TEXT, salary REAL)"""
)

c.execute(
    """CREATE TABLE IF NOT EXISTS companies
             (id INTEGER PRIMARY KEY, name TEXT, staff REAL)"""
)

c.execute(
    """CREATE TABLE IF NOT EXISTS customers
             (id INTEGER PRIMARY KEY, name TEXT, sales REAL)"""
)

# Commit the changes
conn.commit()
```

## Output

### List tables in database
This script uses the sqlite3 module to connect to the specified SQLite database file (db_file) and execute a SQL query to retrieve the names of all tables in the database. The names of the tables are returned as a list of tuples, with each tuple containing the name of a table.

You can change the database name and run the script to get the table names from the database.


```python
def list_tables(db_file):
    conn = sqlite3.connect(db_file)
    c = conn.cursor()
    c.execute("SELECT name from sqlite_master WHERE type='table';")
    tables = c.fetchall()
    conn.close()
    return tables


print(list_tables(db_name))
```
