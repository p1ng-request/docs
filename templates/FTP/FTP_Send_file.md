<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FTP/FTP_Send_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FTP+-+Send+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #ftp #file #naas_drivers #operations #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to securely transfer files to a remote server using the File Transfer Protocol (FTP).

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
