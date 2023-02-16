<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pillow/Pillow_Create_new_image.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pillow+-+Create+new+image:+Error+short+description">Bug report</a>

**Tags:** #pillow #opendata #snippet #data #image

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates and saves an image using Pillow. You can setup its width, height and background color.

<u>References:</u>
- https://holypython.com/python-pil-tutorial/how-to-create-a-new-image-with-pil/

## Input

### Import libraries


```python
from PIL import Image
```

### Setup variables


```python
# Inputs
background_color = "#00004c"
width = 1200
height = 600

# Outputs
output_image = "new_image.png"
```

## Model

### Create new image


```python
img = Image.new("RGB", (width, height), background_color)
display(img)
```

## Output

### Save image


```python
img.save(output_image)
```
