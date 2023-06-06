<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_Create_directory.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+Create+directory:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #snippet #python #operations

**Author:** [Moemen Ebdelli](https://www.linkedin.com/in/moemen-ebdelli)

**Description:** This notebook provides instructions on how to create a directory in Python.

**References:**
- [OS Module Python Tutorial](https://pythonprogramming.net/python-3-os-module/)
- [os — Miscellaneous operating system interfaces](https://docs.python.org/3/library/os.html)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `parent_dir`: Parent Directory path -> provide an absolute or relative path
- `directory`: Directory name


```python
parent_dir = "./"
directory = "MyDir"
```

## Model

### Create Directory


```python
# Prepare the Path
path = os.path.join(parent_dir, directory)

# Create the directory MyDir under awesome-notebooks/Python
try:
    os.mkdir(path)
    msg = "Directory " + directory + " is created under " + parent_dir
except OSError as error:
    msg = "Directory was not created  : " + str(error)
```

## Output

### Print the execution message


```python
print(msg)
```
