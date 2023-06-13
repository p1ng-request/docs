<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_Check_path_exist.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+Check+path+exist:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #python #path #file #system #library #snippet #operations #check

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will show how to check a path exist using os library.

**References:**
- [os.path.exists() method](https://www.geeksforgeeks.org/python-os-path-exists-method/)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `path`:  file path in your local system. If you are using Naas you should start with `/home/ftp` to locate your file


```python
path = '/home/ftp/__templates__' # Specify path
```

## Model

### Check if path exists
This function will check the precise location of the file or directory in a file system you put in the variable


```python
is_exist = os.path.exists(path) # Check whether the specified path exists or not
```

## Output

### Display result


```python
print("Is the path existing ?")
print(is_exist)
```
