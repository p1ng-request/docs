    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Get_last_file_modified_from_directy.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Get+last+file+modified+from+directy:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #os #library #file #modified #directory

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get the last file modified from a directory using the os library.

**References:**
- [os library documentation](https://docs.python.org/3/library/os.html)
- [os.listdir() documentation](https://docs.python.org/3/library/os.html#os.listdir)

## Input

### Import libraries


```python
import os
```

### Setup Variables


```python
# Set the directory path
directory_path = "./"
```

## Model

### Get last file modified


```python
# Get the list of files in the directory
files_list = os.listdir(directory_path)
# Get the last file modified
last_file_modified = max(files_list, key=os.path.getmtime)
```

## Output

### Display result


```python
# Print the last file modified
print(f"The last file modified is {last_file_modified}")
```

 
