<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PowerPoint/PowerPoint_Add_Slide_With_Textbox.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PowerPoint+-+Add+Slide+With+Textbox:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #powerpoint #slide #portrait #pptx #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to create a new slide in PowerPoint with a textbox.

## Input

### Import libraries


```python
try:
    from pptx import Presentation
except:
    !pip install python-pptx --user
    from pptx import Presentation
from pptx.util import Inches, Pt
```

### Setup Variables


```python
output_pptx = "MyPowerPoint_Slide_Textbox.pptx"
text1 = "This is text inside a textbox"
text2 = "This is a second paragraph that's bold"
text3 = "This is a third paragraph that's big"
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

### Add slide with textbox


```python
slide = prs.slides.add_slide(blank_slide_layout)

left = top = width = height = Inches(1)
txBox = slide.shapes.add_textbox(left, top, width, height)
tf = txBox.text_frame

tf.text = text1

p = tf.add_paragraph()
p.text = text2
p.font.bold = True

p = tf.add_paragraph()
p.text = text3
p.font.size = Pt(40)
```

## Output

### Save presentation


```python
prs.save(output_pptx)
```
