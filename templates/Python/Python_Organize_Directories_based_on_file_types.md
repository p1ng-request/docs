<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Organize_Directories_based_on_file_types.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Organize+Directories+based+on+file+types:+Error+short+description">Bug report</a>

**Tags:** #organize #files #directories

**Author:** [Ahmed Mousa](https://www.linkedin.com/in/akmousa/)

**Description:** This notebook organizes your files based on their extensions to directories for data scientists

## Input

### Import libraries


```python
from shutil import move
from os import path
import os
import glob
import pathlib
```

### Variables


```python
files_path = '' #Put the path to where your unorganized files are # Leave it as it's if your files are in the same folder with this notebook
```


```python
exclude_files = [] # Add files to exclude from moving as you wish here in this list
exclude_files.append("Python_Organize_Directories_based_on_file_types.ipynb")
```


```python
folders_extension = {
    'Programming Files': ['ipynb', 'py', 'java', 'cs', 'js', 'vsix', 'jar', 'cc', 'ccc', 'html', 'xml', 'kt'],
    'Data': {'Structured Data':['txt', 'pdf', 'doc', 'pdf', 'ppt', 'pps', 'docx', 'pptx','csv','xlsx','xlsm','xlsb','xltx',
                                  'xltm','xls','xlt','xls','xml','xla','xlam','xlw','xlr'],
    'Unstructured Data':{'Images':['jpeg', 'jpg', 'png', 'gif', 'tiff', 'raw', 'webp', 'jfif', 'ico', 'psd', 'svg', 'ai'],
                          'Videos':['mp4', 'webm', 'mkv', 'MPG', 'MP2', 'MPEG', 'MPE', 'MPV', 'OGG', 'M4P', 'M4V', 'WMV', 'MOV', 'QT', 'FLV', 'SWF', 'AVCHD', 'avi', 'mpg', 'mpe', 'mpeg', 'asf', 'wmv', 'mov', 'qt', 'rm'],
                          'Audio': ['mp3', 'wav', 'wma', 'mpa', 'ram', 'ra', 'aac', 'aif', 'm4a', 'tsa']},
    'Compressed': ['zip', 'rar', 'arj', 'gz', 'sit', 'sitx', 'sea', 'ace', 'bz2', '7z']
            }
}
```

## Model


```python
def create_folder(folder_name):
    if not os.path.exists(folder_name):
        os.makedirs(folder_name)
```


```python
def move_file(file_path,desired_folder_path):
        if not file_path in exclude_files:
            create_folder(desired_folder_path)
            move(file_path,desired_folder_path)
            print(f"Moved file: {file_path}, to {desired_folder_path}")
```


```python
def organize_files():
    for file in glob.glob(files_path+"*"):
        if os.path.isdir(file):
            continue
        file_name_path = file
        file_extiension = pathlib.Path(file).suffix.replace('.',"")
        for folder in folders_extension.keys():
            if isinstance(folders_extension[folder],list):
                if file_extiension in folders_extension[folder]:
                    target_folder_path = os.path.join(files_path,folder)
                    move_file(file,target_folder_path)
            else:
                if isinstance(folders_extension[folder],list):
                    for sub_folder in folders_extension[folder]:
                        if file_extiension in folders_extension[folder][sub_folder]:
                            target_folder_path = os.path.join(files_path,folder,sub_folder)
                            move_file(file,target_folder_path)
                else:
                    for sub_folder in folders_extension[folder]:
                        if isinstance(folders_extension[folder][sub_folder],list):
                                if file_extiension in folders_extension[folder][sub_folder]:
                                    target_folder_path = os.path.join(files_path,folder,sub_folder)
                                    move_file(file,target_folder_path)
                        else:
                            for ssub_folder in folders_extension[folder][sub_folder]:
                                if file_extiension in folders_extension[folder][sub_folder][ssub_folder]:
                                    target_folder_path = os.path.join(files_path,folder,sub_folder,ssub_folder)
                                    move_file(file,target_folder_path)
                        
                
```

## Output


```python
organize_files()
```
