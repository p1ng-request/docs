<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_Remove_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+Remove+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #python #remove #file #system #library #snippet #operations

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to remove file from system using os library.

**References:**
- [os library documentation](https://docs.python.org/3/library/os.html)
- [os.remove() documentation](https://docs.python.org/3/library/os.html#os.remove)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `file_path`: path of the file to be removed


```python
file_path = "untitled.txt"
```

## Model

### Remove file
This function will remove the file from the system.


```python
os.remove(file_path)
```

## Output

### Display result


```python
print(f"The file '{file_path}' has been removed from the system.")
```
