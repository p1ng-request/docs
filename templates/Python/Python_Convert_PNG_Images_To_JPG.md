    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_PNG_Images_To_JPG.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+PNG+Images+To+JPG:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #jpg #png #to #image #images #convert

**Author:** [Ahmed Mousa](https://www.linkedin.com/in/akmousa/)

**Description:** This notebook converts png images to jpg images.

## Input

### Import libraries


```python
from PIL import Image
```

### Setup Variables
Make sure you put your file absolute path or put the file within this notebook directory.


```python
file_path = "Put your file path here / Make sure it's withing this notebook dire"
```

## Model

### Open image and converts to RGB colors


```python
img_png = Image.open(file_path)
img_png = img_png.convert("RGB")
```

Replacing file name extensions


```python
new_file_path = file_path.replace("png", "jpg")
```

## Output

### Save result as jpg file


```python
img_png.save(new_file_path)
```
