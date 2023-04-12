<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/ZIP/ZIP_Extract_files.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=ZIP+-+Extract+files:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #zip #extract #file #operations #snippet #naas

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** This notebook allows users to extract files from a ZIP archive.

## Input

### Import libraries


```python
import zipfile
import os
from pprint import pprint
```

### Setup Variables
- `file_path`: zip archive file path
- `output_dir`: directory name in which files will be extracted


```python
# Inputs
file_path = "files.zip"

# Outputs
output_dir = "zip_extraction"
```

## Model

### Extract files
In this example, `file_path` is the path of the ZIP archive that you want to extract. 
The with statement is used to ensure that the ZIP file is closed properly after it has been read. 
The ZipFile class is used to open the file in read mode ('r'). 
The extractall method is called to extract all the files in the archive to the current working directory. 
You can also specify a different directory to extract the files to by passing a path to the extractall method.


```python
# Create output dir
os.mkdir(output_dir)

# Extract files
if os.path.exists(file_path):
    # open the zip file for reading
    with zipfile.ZipFile(file_path, 'r') as zip_ref:
        # extract all files to the current working directory
        zip_ref.extractall(output_dir)
else:
    print(f"❌ ZIP path '{file_path}' does not exist. Please update it on your variables.")
```

## Output

### Display result


```python
print("Number of files extracted:", len(os.listdir(output_dir)))
pprint(os.listdir(output_dir))
```
