<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OwnCloud/OwnCloud_Download_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OwnCloud+-+Download+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #owncloud #cloud #storage #operations #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to download files from their OwnCloud account.

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
oc = owncloud.Client("https://cloud.damken.com")

oc.login("YOURNAME", "YOURPASS")
```

## Output

### Get file from your ownCloud


```python
oc.get_file("testdir/download_to_owncloud.ipynb", "download_to_owncloud.ipynb")
```
