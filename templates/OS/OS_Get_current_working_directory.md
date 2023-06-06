<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_Get_current_working_directory.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+Get+current+working+directory:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #python #snippet #operations #operatingsystem

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook demonstrates how to get the current working directory using `os` module. The main purpose of the OS module is to interact with your operating system. The primary use I find for it is to create folders, remove folders, move folders, and sometimes change the working directory. You can also access the names of files within a file path by doing listdir(). We do not cover that in this video, but that's an option.

**References:**
- [OS Module Python Tutorial](https://pythonprogramming.net/python-3-os-module/)
- [os — Miscellaneous operating system interfaces](https://docs.python.org/3/library/os.html)

## Input

### Import libraries


```python
import os
```

## Model

### Get current working directory
The os.getcwd() function returns the current working directory of the process.


```python
# Get the current working directory
cwd = os.getcwd()
```

## Output

### Display result


```python
# Print the current working directory
print(cwd)
```

 
