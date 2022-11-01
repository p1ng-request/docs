<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PowerPoint/PowerPoint_Add_title_%2B_line_in_presentation.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PowerPoint+-+Add+title+++line+in+presentation:+Error+short+description">Bug report</a>

**Tags:** #powerpoint #naas #python #python_pptx

**Author:** [Ayoub Berdeddouch](https://www.linkedin.com/in/ayoub-berdeddouch)

**Description:** This notebook Adds a title + Line to a presentation in PowerPoint

## Input

### Import libraries

* Installation : https://pypi.org/project/python-pptx/
* **pptx documentation : https://python-pptx.readthedocs.io/en/latest/api/presentation.html**


```python
 !pip install python-pptx
```


```python
from pptx import Presentation
from pptx.enum.shapes import MSO_CONNECTOR
from pptx.util import Inches
```

### Variables


```python
#Create blank PowerPoint file
prs = Presentation()

#set slide template labels. This just makes is easier to read the code. The layout index can also be used.                   
SLD_LAYOUT_TITLE = 0
SLD_LAYOUT_TITLE_AND_CONTENT = 1
SLD_LAYOUT_TITLE_ONLY = 5
```

## Model

### Create a title and a line within the Presentation


```python
#Set title page text variables
slide_title = "Jupyter Notebooks-as-a-service"
# slide_subtitle = dt.datetime.today().strftime('%m/%d/%Y')

# slide_subtitle = "All-in-one open source data platform, based on @jupyter"
#Add a title slide
slide_layout = prs.slide_layouts[SLD_LAYOUT_TITLE]
slide = prs.slides.add_slide(slide_layout)

#Insert title slide text. There are two text shapes on the Title slide layout by default.
slide.shapes[0].text = slide_title
# slide.shapes[1].text = slide_subtitle
```


```python
# function to create slide with title and a line
def pptx_slide(title="Title"):
    #Create blank PowerPoint file
    prs = Presentation()

    #set slide template labels. This just makes is easier to read the code. The layout index can also be used.                   
    SLD_LAYOUT_TITLE = 0
    SLD_LAYOUT_TITLE_AND_CONTENT = 1
    SLD_LAYOUT_TITLE_ONLY = 5
    
    #Set title page text variables
    slide_title = title
    # slide_subtitle = dt.datetime.today().strftime('%m/%d/%Y')

    
    #Add a title slide
    slide_layout = prs.slide_layouts[SLD_LAYOUT_TITLE_ONLY]
    slide = prs.slides.add_slide(slide_layout)

    #Insert title slide text. There are two text shapes on the Title slide layout by default.
    slide.shapes[0].text = slide_title
    
       
    # Inserting the line
    line1=slide.shapes.add_connector(MSO_CONNECTOR.STRAIGHT, Inches(7.0), Inches(2.0), Inches(1.5), Inches(2.0))
    
    # save the presentation
    prs.save("Presentation_Title_Line.pptx")
```

## Output

### Save result in csv


```python
# save with the function
pptx_slide("NaaS: Jupyter Notebooks-as-a-service")
```


```python

```
