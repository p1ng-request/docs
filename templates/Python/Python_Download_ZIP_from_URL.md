<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Download_ZIP_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Download+ZIP+from+URL:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #urllib #download #zip #url #request

**Author:** [Hamid Mukhtar](https://www.linkedin.com/in/mukhtar-hamid/)

**Description:** This notebook will show how to download a ZIP file from a URL using urllib.request.

**References:**
- [urllib.request documentation](https://docs.python.org/3/library/urllib.request.html)
- [urllib.request tutorial](https://www.pythonforbeginners.com/urllib/urllib-tutorial)

## Input

### Import libraries


```python
import os
import shutil
import urllib
```

### Setup Variables
- `url`: desired url from which we have to download the zip file
- `headers_1`: passing the user agent to surpass the request
- `output_path`: path of the file to be save


```python
# Inputs 
url = 'https://www.learningcontainer.com/wp-content/uploads/2020/05/sample-zip-file.zip'
headers_1 = {'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36'}

# Outputs
output_path = "MyFile.zip"
```

## Model

### Download zip files
In this example, `url` is the path of the ZIP file that we want to download. 
The with statement is used to ensure that the ZIP file is closed properly after it has been read & written. 
The urllib.request.Request class is used to request the file. 
The urllib.request.urlopen method is called to open all the files in the archive to the current working directory. 
The shutil.copyfileobj class is used to open all the files and copy it in the required file as `MyFile.zp` as f.


```python
# request the file from website
req = urllib.request.Request(url, headers=headers_1)

# open it in a file and write it to save it in local
with urllib.request.urlopen(req) as response, open(output_path, 'wb') as f:
    shutil.copyfileobj(response, f)
```

## Output

### Display result

The ZIP file has been downloaded and saved in the current directory.


```python
print("✅ ZIP downloaded on:", output_path)
```

 

 
