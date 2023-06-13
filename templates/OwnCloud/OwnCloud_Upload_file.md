<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OwnCloud/OwnCloud_Upload_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OwnCloud+-+Upload+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #owncloud #cloud #storage #operations #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to securely upload files to their own personal cloud storage.

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

### Create a folder


```python
oc.mkdir("testdir")
```

### Upload this file to your ownCloud


```python
oc.put_file("testdir/upload_to_owncloud.ipynb", "upload_to_owncloud.ipynb")
```

### Get sharable link to the file


```python
link_info = oc.share_file_with_link("testdir/upload_to_owncloud.ipynb")
```

## Output

### Display result


```python
print("Here is your link: " + link_info.get_link())
```


```python

```
