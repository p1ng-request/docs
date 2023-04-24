<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_Create_a_Slide.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+Create+a+Slide:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googleslides #slides #create #api #developers #guides

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook describes how to insert a blank slide to an existing Google Slides presentation establishing a seamless connection using OAuth consent.

**References:**
- [Google Slides API Guides](https://developers.google.com/slides/api/guides/create-slide)

## Input

### Import libraries


```python
try:
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
except ModuleNotFoundError:
    !pip install google-api-python-client
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
import requests
import uuid
```

### Setup Variables
- `secret_path`: Set the path to the credentials JSON file
- `scopes`: Set the scopes required for accessing Google Slides
- `presentation_url`: The URL of the presentation to add the slide to.
- `insertion_index`: Specify the position at which you want to insert the slide


```python
# Inputs
secret_path = 'secret.json'
scopes = ['https://www.googleapis.com/auth/presentations', 'https://www.googleapis.com/auth/presentations.readonly']
presentation_url = "https://docs.google.com/presentation/d/1bH9tJgfGIqwzDvhst8rLxmI12efwmsWsbWenKZNRf7s/edit#slide=id.SLIDES_API1712173254_0"
insertion_index = 1  # Replace with the actual position where you want to insert the slide
```

## Model

### Connect to client


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
slides_service = build('slides', 'v1', credentials=credentials)
```

## Output

### Create Slide


```python
# Get the presentation ID from URL
presentation_id = presentation_url.split("/d/")[-1].split("/")[0]

# Generate a unique object ID for the duplicated slide
new_slide_id = f'{str(uuid.uuid4())[:50]}'

# Duplicate the slide
requests = [
    {
        'createSlide': {
            'objectId': new_slide_id,
            'slideLayoutReference': {
                'predefinedLayout': 'BLANK'
            },
            'insertionIndex': insertion_index,
        }
    }
]

# Execute the batch update request
slides_service.presentations().batchUpdate(presentationId=presentation_id, body={'requests': requests}).execute()
print('Slide created successfully!', f"https://docs.google.com/presentation/d/{presentation_id}/edit#slide=id.{new_slide_id}")
```

 
