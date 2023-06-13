<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OS/OS_List_entries_in_directory.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OS+-+List+entries+in+directory:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #os #listdir #directory #python #entries #list

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook explains how to use the Python method listdir() to list entries in a directory. It is usefull for organizations to quickly access the content of a directory.

**References:**
- [Python OS Listdir](https://www.tutorialspoint.com/python/os_listdir.htm)
- [Python OS Module](https://docs.python.org/fr/3/library/os.html)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `directory`: path of the directory to list entries


```python
directory = '/home/ftp/'
```

## Model

### List entries in directory

Python method listdir() returns a list containing the names of the entries in the directory given by path. The list is in arbitrary order. It does not include the special entries '.' and '..' even if they are present in the directory.


```python
entries = os.listdir(directory)
```


This code snippet separates directory entries into files and subdirectories It creates two empty lists, `files` and `subdirectories`, and browses the entries. If an entry is a file, it is added to the `files` list. If it's a subdirectory, it's added to the `subdirectories` list.


```python
# Separate files and subdirectories
files = []
subdirectories = []

for entry in entries:
    if os.path.isfile(os.path.join(directory, entry)):
        files.append(entry)
    else:
        subdirectories.append(entry)
```

## Output

### Display result


```python
# Print the list of files
print("Files:")
for file in files:
    print("- {}".format(file))

# Print the list of subdirectories
print("Subdirectories:")
for subdirectory in subdirectories:
    print("- {}".format(subdirectory))
```

 
