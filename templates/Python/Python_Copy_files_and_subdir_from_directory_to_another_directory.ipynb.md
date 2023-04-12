<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Copy_files_and_subdir_from_directory_to_another_directory.ipynb.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Copy+files+and+subdir+from+directory+to+another+directory:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #os #shutil #operations #snippet

**Author:** [Parth Panchal](https://www.linkedin.com/in/parthpanchal8401/)

**Description:** This notebook provides a Python script to copy files and subdirectories from one directory to another.

## Input

### Import libraries


```python
import shutil
import os
```

### Setup Variables
- `source_folder`: Path of your source directory
- `overwrite`: Overwrite files in destination, (default=True)
- `destination_folder`: Path of your destination directory


```python
# Inputs
source_folder = ".."
overwrite = True

# Outputs
destination_folder = "."
```

## Model

### Copy files and subdir from directory to another directory


```python
def copy_all_files(dir_src, dir_des, overwrite=True):
    """
    dir_src: Path of your source directory
    dir_des : Path of your destination directory
    overwrite: Overwrite files in destination, (default=True)
    """
    # Check if source and destination folders exists
    if not os.path.exists(dir_src):
        print("❌ Source folder does not exist:", dir_src)
        return None
    
    if not os.path.exists(dir_des):
        print("❌ Destination folder does not exist:", dir_des)
        return None
    
    # Copy files
    for root, dirs, files in os.walk(dir_src):
        for file in files:
            path_file = os.path.join(root, file)
            file_from_dir = path_file.replace(dir_src, "")
            dest_path = os.path.join(dir_des, file_from_dir[1:])
            if not overwrite:
                if not os.path.exists(dest_path):
                    try:
                        shutil.copy(path_file, dest_path)
                        print(f"✅ Copied file: {path_file}")
                    except IOError as io_err:
                        os.makedirs(os.path.dirname(dest_path))
                        shutil.copy(path_file, dest_path)
                else:
                    print(f"❎ File already exists: {dest_path}")
            else:
                if os.path.exists(dest_path):
                    os.remove(dest_path)
                try:
                    shutil.copy(path_file, dest_path)
                    print(f"✅ Copied file: {path_file}")
                except IOError as io_err:
                    os.makedirs(os.path.dirname(dest_path))
                    shutil.copy(path_file, dest_path)
```

## Output

### Copy all files


```python
copy_all_files(source_folder, destination_folder, overwrite=overwrite)
```
