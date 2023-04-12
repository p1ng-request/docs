<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Start+data+product:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #dataproduct #automation

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** In this notebook, we'll walk you through the process of starting a data product using the Naas data product framework and integrating awesome-notebooks into your project. 

Please note that this notebook can only be used while connected to your Naas account. If you'd like to perform these steps locally, please don't hesitate to contact us – we're more than happy to assist you.

**References:**
- [Data Product Framework](https://github.com/jupyter-naas/data-product-framework)
- [Naas Documentation](https://docs.naas.ai/)

## Input

### Import libraries


```python
import urllib.request
import zipfile
import glob
import os
import shutil
import pandas as pd
import re
```

### Setup Variables
- `product_name`: Name of your data product in lower cases without space
- `notebooks`: List of awesome-notebooks name to be added into models/basic to kick start your data product.


```python
product_name = "my-first-data-product"
notebooks = [
    "Naas_Create_Pipeline.ipynb",
    "Naas_Add_Scheduler.ipynb",
    "Naas_Delete_Scheduler.ipynb",
]
```

## Model

### Clean data product name


```python
product_name = product_name.lower().replace(" ", "-")
print("✅ Data product name:", product_name)
```

### Download data product framework repository (ZIP)


```python
zip_url = f"https://github.com/jupyter-naas/data-product-framework/archive/refs/heads/master.zip"
output_dir = f"/home/ftp/{product_name}.zip"
urllib.request.urlretrieve(zip_url, output_dir)
print("✅ Data Product Framework ZIP downloaded:", output_dir)
```

### Unzip and rename reposistory


```python
with zipfile.ZipFile(output_dir, 'r') as zip_ref:
    # extract files on root dir
    zip_ref.extractall("/home/ftp/")
    
current_folder_name = f"/home/ftp/data-product-framework-main"
new_folder_name = f"/home/ftp/{product_name}"

# Rename the folder
i = 1
while True:
    if os.path.exists(new_folder_name):
        new_folder_name = f"{new_folder_name}_{i}"
        i += 1
    else:
        break
os.rename(current_folder_name, new_folder_name)
print("✅ Folder unzip:", new_folder_name)
```

### Remove ZIP


```python
os.remove(output_dir)
print("✅ Data Product Framework ZIP removed from root folder")
```

### Copy Awesome-notebooks to your data product


```python
# Get all templates
templates_path = sorted(glob.glob("/home/ftp/__templates__/*/*.ipynb", recursive=True))
df_templates = pd.DataFrame({"TEMPLATE_PATH": templates_path})
df_templates["TEMPLATE_NAME"] = df_templates.apply(lambda row: row["TEMPLATE_PATH"].split("/")[-1], axis=1)
print("Templates found:", len(df_templates))

for notebook in notebooks:
    if notebook.endswith(".ipynb") and notebook in df_templates["TEMPLATE_NAME"].unique():
        notebook_path = df_templates.loc[df_templates["TEMPLATE_NAME"] == notebook, "TEMPLATE_PATH"].values[0]
        dst_file = f"{new_folder_name}/models/basic/{notebook}"
        shutil.copy2(notebook_path, dst_file)
        print(f"✅ Notebook '{notebook_path}' copied to '{dst_file}'")      
```

## Output

### Display result


```python
print("✅ You can now started working on your new data product:", new_folder_name)
```
