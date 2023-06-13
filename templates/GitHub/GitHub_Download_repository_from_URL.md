<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Download_repository_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Download+repository+from+URL:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #download #repository #url #api #zip

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to download a repository from a URL.

**References:**

## Input

### Import libraries


```python
import requests
import urllib
import os
import zipfile
```

### Setup Variables
- `url`: URL of the repository to be downloaded
- `branch_master`: Name of the master branch
- `output_dir`: Path of the directory as output


```python
# Inputs
url = "https://github.com/jupyter-naas/data-product-framework"
branch_master = "master"

# Outputs
output_dir = "."
```

## Model

### Download repository


```python
repo_name = url.split("/")[-1].split("/")[0]
zip_url = f"{url}/archive/refs/heads/{branch_master}.zip"
output_path = os.path.join(output_dir, f"{repo_name}.zip")
urllib.request.urlretrieve(zip_url, output_path)
print("✅ Repo archive downloaded:", output_path)
```

### Unzip and rename reposistory


```python
with zipfile.ZipFile(output_path, 'r') as zip_ref:
    # extract files on root dir
    zip_ref.extractall(output_dir)
print("✅ Folder unzip")
```

### Remove ZIP


```python
os.remove(output_path)
print("✅ ZIP removed from root folder")
```

## Output

### Display result


```python
print("✅ Repo downloaded available in dir:", output_dir)
```
