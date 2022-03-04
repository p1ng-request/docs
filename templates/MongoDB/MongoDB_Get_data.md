<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# MongoDB - Get data
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/MongoDB/MongoDB_Get_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #mongodb #database #naas_drivers

## Input

### Import library


```python
import naas
```

### Variables


```python
user = "my user"
passwd = "my passwd"
host = "url"
port = 9090
collection_name = "col"
db_name = "db_name"
```

## Model

### Connect


```python
ftp = naas_drivers.mongo.connect(host, port, user, passwd)
```

## Output

### Get Data


```python
naas_drivers.mongo.get(collection_name, db_name)
```
