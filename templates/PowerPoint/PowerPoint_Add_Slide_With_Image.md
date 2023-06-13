<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PowerPoint/PowerPoint_Add_Slide_With_Image.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PowerPoint+-+Add+Slide+With+Image:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #powerpoint #slide #portrait #pptx #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides instructions on how to add an image to a PowerPoint slide.

## Input

### Import libraries


```python
try:
    from pptx import Presentation
except:
    !pip install python-pptx --user
    from pptx import Presentation
from pptx.util import Inches
```

### Setup Variables


```python
output_pptx = "MyPowerPoint_Slide_Image.pptx"
img_path = "1664217502406.jfif"
```

## Model

### Create Presentation Obj


```python
prs = Presentation()
```

### Setup Width & Height (Portrait)


```python
prs.slide_height = Inches(11.69)
prs.slide_width = Inches(8.27)
```

### Setup Layout


```python
blank_slide_layout = prs.slide_layouts[6]
```

### Add slide 1 with Image


```python
slide1 = prs.slides.add_slide(blank_slide_layout)

left = top = Inches(1)
pic = slide1.shapes.add_picture(img_path, left, top)
```

### Add slide 2 with Image


```python
slide2 = prs.slides.add_slide(blank_slide_layout)

left = Inches(5)
height = Inches(5.5)
pic = slide2.shapes.add_picture(img_path, left, top, height=height)
```

## Output

### Save presentation


```python
prs.save(output_pptx)
```
