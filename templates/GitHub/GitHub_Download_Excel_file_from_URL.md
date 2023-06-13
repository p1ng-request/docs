<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Download_Excel_file_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Download+Excel+file+from+URL:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #excel #download #url #file #python

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to download an Excel file stored on a GitHub repository.

**References:**
- [GitHub API Documentation](https://developer.github.com/v3/)
- [Python Requests Library](https://requests.readthedocs.io/en/master/)

## Input

### Import libraries


```python
import requests
import pandas as pd
```

### Setup Variables
- `url`: URL of the Excel file stored on GitHub
- `output_path`: Name of the output to be saved on your local


```python
# Inputs
url = "https://github.com/jupyter-naas/awesome-notebooks/blob/master/Excel/Conso.xlsx"

# Outputs
output_path = "Excel.xlsx"
```

## Model

### Download Excel file


```python
def download_excel_file(url, output_path):
    # Check URL
    if not url.endswith("?raw=true") and url.endswith(".xlsx"):
        url = f'{url}?raw=true'
        
    # Get file
    response = requests.get(url)
    with open(output_path, "wb") as f:
        f.write(response.content)
    print("✅ Excel file successfully saved:", output_path)
```

## Output

### Display result


```python
download_excel_file(url, output_path)
```
