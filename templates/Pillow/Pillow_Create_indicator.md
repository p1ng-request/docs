<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pillow/Pillow_Create_indicator.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pillow+-+Create+indicator:+Error+short+description">Bug report</a>

**Tags:** #pillow #opendata #snippet #data #image #indicator #kpi

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates an indicator with title and kpi using Pillow.

<u>References:</u>
- https://holypython.com/python-pil-tutorial/how-to-create-a-new-image-with-pil/
- https://holypython.com/python-pil-tutorial/how-to-add-text-to-images-in-python-via-pil-library/
- https://holypython.com/python-pil-tutorial/how-to-open-show-and-save-images-in-python-pil/

## Input

### Import libraries


```python
from PIL import Image, ImageDraw, ImageFont
import urllib
```

### Setup variables


```python
# Inputs
title = "My title"
title_font_name = "https://github.com/jupyter-naas/awesome-notebooks/blob/master/Pillow/ArchivoBlack-Regular.ttf"  # font in Local or GitHub link
title_font_size = 40

indicator = "My indicator"
indicator_font_name = "https://github.com/jupyter-naas/awesome-notebooks/blob/master/Pillow/ArchivoBlack-Regular.ttf"  # font in Local or GitHub link
indicator_font_size = 90

pad = 50  # additional space between title and indicator
width = 1200
height = 600
background_color = "#00004c"

# Outputs
output_image = "Pillow_indicator.png"
```

## Model

### Download font in local


```python
def download_github_file(url):
    if not url.endswith("?raw=true"):
        url = f"{url}?raw=true"
    response = urllib.request.urlopen(url)
    filepath = url.split("/")[-1].split("?raw=true")[0]
    file = open(filepath, "wb")
    file.write(response.read())
    file.close()
    return filepath
```

### Create indicator


```python
def create_indicator(
    title="My title",
    title_font_name="https://github.com/jupyter-naas/awesome-notebooks/blob/master/Pillow/ArchivoBlack-Regular.ttf",
    title_font_size=40,
    indicator="My Indicator",
    indicator_font_name="https://github.com/jupyter-naas/awesome-notebooks/blob/master/Pillow/ArchivoBlack-Regular.ttf",
    indicator_font_size=90,
    pad=50,
    width=1200,
    height=600,
    background_color="#043D57",
):
    # Download font if not in local
    title_font_name = download_github_file(title_font_name)
    indicator_font_name = download_github_file(indicator_font_name)

    # Create image background
    img = Image.new("RGB", (width, height), background_color)
    draw = ImageDraw.Draw(img)

    # Title
    font_1 = ImageFont.truetype(title_font_name, title_font_size)
    w1, h1 = draw.textsize(title, font=font_1)

    # indicator
    font_2 = ImageFont.truetype(indicator_font_name, indicator_font_size)
    w2, h2 = draw.textsize(indicator, font=font_2)

    # Text position
    x1 = width / 2
    y1 = (height / 2) - h1 - (h2 / 2)

    x2 = width / 2
    y2 = (height / 2) - h1 + pad

    draw.text((x1, y1), title, font=font_1, anchor="mm")
    draw.text((x2, y2), indicator, font=font_2, anchor="mm")
    return img


img = create_indicator(
    title,
    title_font_name,
    title_font_size,
    indicator,
    indicator_font_name,
    indicator_font_size,
    pad,
    width,
    height,
    background_color,
)
display(img)
```

## Output

### Save image


```python
img.save(output_image)
```
