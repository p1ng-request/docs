<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# OwnCloud - Download file
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OwnCloud/OwnCloud_Download_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #owncloud #cloud #storage

## Input

### Install packages


```python
!pip install pyocclient
```

### Import library


```python
import naas
import owncloud
```

## Model

### Connect to your ownCloud


```python
oc = owncloud.Client('https://cloud.damken.com')

oc.login('YOURNAME', 'YOURPASS')
```

## Output

### Get file from your ownCloud


```python
oc.get_file('testdir/download_to_owncloud.ipynb', 'download_to_owncloud.ipynb')
```
