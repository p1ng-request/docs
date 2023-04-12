<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/SQLite/SQLite_Create_Database_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=SQLite+-+Create+Database+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #SQLite #database #databasemanagement #filebaseddb #dbcreation #dbsetup #SQLiteDB #localstorage #datastore #SQLitedatabase #embeddedDB #PythonDB #sqllite3 #DBfile

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates a new SQLite database file using the sqlite3 module in Python. Here's an example of how you can create a new SQLite database file called "mydatabase.db"

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

### Create database file
In this example, the connect() function is used to connect to a SQLite database file called "mydatabase.db". If the file does not exist, it will be created.
Once the connection is made, the connection object returned by the connect() function can be used to execute SQL statements and perform other operations on the database.

Please note that creating a new database file with sqlite3 module in python, won't create any tables or data inside it. To do so, you will need to create tables and insert data using sql statement.

Please also keep in mind that python does not make any directories for the database file, So make sure the path specified for the connection string is valid and exists.


```python
# connect to the database file
conn = sqlite3.connect(db_name)
```

## Output

### Close the connection


```python
# close the connection
conn.close()
```
