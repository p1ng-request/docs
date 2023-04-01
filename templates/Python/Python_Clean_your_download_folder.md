<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Clean_your_download_folder.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Clean+your+download+folder:+Error+short+description">Bug report</a>

**Tags:** #python #automation #clean_folder

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook will go through your given folder and check each file last modification time, and if it's been more than 30 days it will move those file to new folder 'files_to_delete'

## Input

### Import libraries


```python
import os
import shutil
from datetime import datetime, timedelta
```

### Setup Variables
- `path`: path of folder to be clean


```python
## taking the folder path to be clean
path = input("Enter the folder path: ")
```


```python
## path of folder to be clean 
folder_path = os.path.join(os.path.expanduser('~'), path)
## path of new folder
to_delete_path = os.path.join(os.path.expanduser('~'), 'files_to_delete')
```


```python
## creating 'to_delete' folder, if does not exists already
if not os.path.exists(to_delete_path):
    os.makedirs(to_delete_path)
```

## Model


```python
## getting list of all the files 
files = os.listdir(folder_path)
```


```python
## getting current time
now = datetime.now()
```


```python
## iterating over the list of files
for file in files:
    ## get the file path
    file_path = os.path.join(folder_path, file)
    
    ## get the file modification date
    modification_date = datetime.fromtimestamp(os.path.getmtime(file_path))
    
    ## calculate the time difference
    time_difference = now - modification_date
    
    ## if the file is older than 30 days 
    ## moving the file to 'to_delete' folder
    if time_difference > timedelta(days=30):
        shutil.move(file_path, to_delete_path)
```

## Output


```python
print("The files has been successfully moved to 'files_to_delete' folder.")
```
