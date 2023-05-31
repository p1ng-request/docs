<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_List_specific_files_from_directory_and_subdirectories.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+List+specific+files+from+directory+and+subdirectories:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #glob #os #files #directory #subdirectories

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook list all specific files from a directory and its subdirectories using glob and os libraries. It is usefull to quickly list all files from a directory and its subdirectories.

**References:**
- [glob module to list files of a directory](https://pynative.com/python-list-files-in-a-directory/#h-glob-module-to-list-files-of-a-directory)
- [os module to list files of a directory](https://pynative.com/python-list-files-in-a-directory/#h-os-module-to-list-files-of-a-directory)

## Input

### Import libraries


```python
import glob
import os
```

### Setup Variables
- `directory`: path of the directory to list files
- `file_extension`: extension of the files to list


```python
directory = "./"
file_extension = "txt"
```

## Model

### List files from directory and subdirectories


```python
files = glob.glob(os.path.join(directory, "**/*." + file_extension), recursive=True)
```

## Output

### Display result


```python
files
```

 
