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

    Files:
    - .gitconfig
    - Python_Convert_URL_to_string.ipynb
    - Naas_Scheduler_demo_(1).ipynb
    - Excel_Save_file.ipynb
    - Gmail_Schedule_mailbox_cleaning.ipynb
    - 108de041-a340-4813-b01f-ef2ee4b8dd68-3329.ipynb
    - Naas_Scheduler_demo.ipynb
    - Python_Convert_URL_to_string_(1).ipynb
    - .bash_history
    Subdirectories:
    - .config
    - Notebooks
    - .ssh
    - .git
    - .cache
    - awesome-notebooks
    - .ipynb_checkpoints
    - .virtual_documents
    - .naas
    - My-workbook
    - .jupyter
    - .ipython
    - .local
    - .npm
    - __tutorials__
    - __production__
    - __templates__


 
