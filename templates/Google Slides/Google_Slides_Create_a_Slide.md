<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_Create_a_Slide.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+Create+a+Slide:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googleslides #slides #create #api #developers #guides

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook describes how to add slides to an existing Google Slides presentation. It is usefull for organizations that need to create slides quickly and easily.

**References:**
- [Google Slides API Guides](https://developers.google.com/slides/api/guides/create-slide)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `presentation_id`: The ID of the presentation to add the slide to.
- `slide_title`: The title of the slide.
- `slide_text`: The text to be added to the slide.


```python
presentation_id = "123456789"
slide_title = "My Slide"
slide_text = "This is my slide text."
```

## Model

### Create Slide

This function creates a slide in an existing Google Slides presentation.


```python
def create_slide(presentation_id, slide_title, slide_text):
    # Create the request body
    body = {
        "requests": [
            {
                "createSlide": {
                    "objectId": slide_title,
                    "insertionIndex": "1",
                    "slideLayoutReference": {"predefinedLayout": "TITLE_AND_BODY"},
                    "slide": {
                        "pageElements": [
                            {
                                "objectId": "title",
                                "shape": {
                                    "placeholder": {"type": "TITLE", "index": "0"},
                                    "text": {
                                        "textElements": [
                                            {"textRun": {"content": slide_title}}
                                        ]
                                    },
                                },
                            },
                            {
                                "objectId": "body",
                                "shape": {
                                    "placeholder": {"type": "BODY", "index": "1"},
                                    "text": {
                                        "textElements": [
                                            {"textRun": {"content": slide_text}}
                                        ]
                                    },
                                },
                            },
                        ]
                    },
                }
            }
        ]
    }
    # Make the request
    response = requests.post(
        f"https://slides.googleapis.com/v1/presentations/{presentation_id}:batchUpdate",
        json=body,
    )
    # Return the response
    return response
```

## Output

### Display result


```python
response = create_slide(presentation_id, slide_title, slide_text)
print(response.status_code)
print(response.json())
```

 
