<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Delete_entire_directory_tree.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Delete+entire+directory+tree:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #shutil #delete #folder #file #directory

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to delete an entire directory tree using the shutil library. 

Shutil module in Python provides many functions of high-level operations on files and collections of files. It comes under Python’s standard utility modules. This module helps in automating the process of copying and removal of files and directories. 

`shutil.rmtree()` is used to delete an entire directory tree, path must point to a directory (but not a symbolic link to a directory).

**References:**
- [shutil documentation](https://docs.python.org/3/library/shutil.html)
- [How to delete a folder in Python](https://www.geeksforgeeks.org/how-to-delete-a-folder-in-python/)

## Input

### Import libraries


```python
import shutil
```

### Setup Variables
- `folder_path`: path of the folder to be removed


```python
folder_path = "./my_folder"
```

## Model

### Delete entire directory tree


```python
shutil.rmtree(folder_path)
```

## Output

### Display result


```python
print(f"Folder {folder_path} deleted.")
```

 
