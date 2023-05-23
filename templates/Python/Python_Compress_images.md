<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Compress_images.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Compress+images:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #PIL #images #compress

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook uses PIL library to compress the image.

## Input

### Import libraries


```python
try:
    from PIL import Image
except:
    !pip install PIL
    from PIL import Image
import os
import requests
```

### Setup Variables

- `image_url`: address of the image file


```python
image_url = "https://source.unsplash.com/user/c_v_r/1900x800"
```

## Model

### Saving the image 


```python
response = requests.get(image_url)
open("image.jpg", "wb").write(response.content)
```


```python
## opening the image to work on
image = Image.open("image.jpg")
```


```python
## getting height and width of image
height, width = image.size
```

### Compressing image


```python
compressed_image = image.resize((height, width), Image.ANTIALIAS)
```


```python
## saving compressed image
compressed_image.save("compressed_image.jpg", optimize=True, quality=9)
```

## Output


```python
## print the size in bytes of original and compressed image
print("Size of original image in bytes:",os.stat('image.jpg').st_size)
print("Size of compressed image in bytes:",os.stat('compressed_image.jpg').st_size)
```
