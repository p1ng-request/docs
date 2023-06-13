<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_Rename_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+Rename+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #python #snippet #operations

**Author:** [Divakar](https://www.linkedin.com/in/divakar-r-9b34b86b/)

**Description:** This notebook will show how to rename file using os library.

**References:**
- [OS Module Python Tutorial](https://pythonprogramming.net/python-3-os-module/)
- [os — Miscellaneous operating system interfaces](https://docs.python.org/3/library/os.html)

## Input 

### Import libraries


```python
import os
```

### Setup Variables
- `input_file_path`: input file path
- `output_file_path`: output file path


```python
input_file_path = "test1.ppt"
output_file_path = "test2.ppt"
```

## Model

### Rename file using os


```python
os.rename(input_file_path, output_file_path)
```

## Output

### Display result


```python
print(f"File {input_file_path} successfully renamed: {output_file_path}!")
```
