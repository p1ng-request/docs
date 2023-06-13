<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FEC/FEC_Lecture_des_fichiers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FEC+-+Lecture+des+fichiers:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fec #lecture #fichiers #python #data #analyse

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to read files with Python and how it is usefull for organization.

**References:**
- [Python Documentation - Reading and Writing Files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
- [Python Documentation - File Objects](https://docs.python.org/3/glossary.html#term-file-object)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `file_name`: Name of the file to read
- `file_path`: Path of the file to read


```python
file_name = "example.txt"
file_path = os.path.join(os.getcwd(), file_name)
```

## Model

### Read file

Long description of the function to read a file without break.


```python
# Open the file
file_object = open(file_path, "r")
# Read the file
file_content = file_object.read()
# Close the file
file_object.close()
```

## Output

### Display result


```python
print(file_content)
```

 
