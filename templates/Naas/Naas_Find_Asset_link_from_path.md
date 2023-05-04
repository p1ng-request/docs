<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Find_Asset_link_from_path.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Find+Asset+link+from+path:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #asset #path #link #find #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will help you find the asset link generated with naas from a given file path.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Asset Documentation](https://docs.naas.ai/features/asset)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `file_path`: File path in naas


```python
file_path = "."
```

## Model

### Find asset link from path


```python
def find_naas_asset_link(file_path):
    if not file_path.startswith("/home/ftp/"):
        file_path = f"/home/ftp/{file_path}"
    asset_link = naas.asset.find(file_path)
    if asset_link:
        print("✅ Asset link found:")
    return asset_link
```

## Output

### Display result


```python
asset_link = find_naas_asset_link(file_path)
print(asset_link)
```

 
