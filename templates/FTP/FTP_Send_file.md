<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# FTP - Send file
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FTP/FTP_Send_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #ftp #file

## Input

### Import library


```python
from naas_drivers import ftp
```

### Variables


```python
path = "/path/to/file/in/ftp"
dest_path = "/path/to/file/in/ftp"
user = "my user"
passwd = "my passwd"
```

## Model

### Connect to ftp


```python
ftp = ftp.connect(user, passwd)
```

## Output

### Send the data


```python
ftp = naas_drivers.ftp.connect(user, passwd)
ftp.send(path, dest_path)
```
