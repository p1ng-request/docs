<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_Duplicate_slide.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+Duplicate+slide:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googleslides #slides #duplicate #copy #presentation #slideshow

**Author:** [Florent Ravenel](https://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to duplicate a slide in Google Slides establishing a seamless connection using OAuth consent. It is usefull for organizations that need to quickly create a presentation with similar slides.

**References:**
- [Google Slides - Duplicate a slide](https://support.google.com/docs/answer/9071445?hl=en)
- [Google Slides - Create a presentation](https://support.google.com/docs/answer/181403?hl=en)

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
import uuid
```

### Setup Variables
- `secret_path`: Set the path to the credentials JSON file
- `scopes`: Set the scopes required for accessing Google Slides
- `slide_url`: The URL of the slide to be duplicated.
- `insertion_index`: Specify the position at which you want to insert the slide


```python
# Inputs
secret_path = 'secret.json'
scopes = [
    'https://www.googleapis.com/auth/presentations',
    'https://www.googleapis.com/auth/presentations.readonly'
]
slide_url = "https://docs.google.com/presentation/d/xxxxxxxxxxxxx/edit#slide=id.xxxxxxxxxx"
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

### Duplicate slide
Duplicate a slide in Google Slides using the slide ID.


```python
# Get presentation_id & slide ID
presentation_id = slide_url.split("/d/")[-1].split("/")[0]
slide_id = slide_url.split("slide=id.")[-1]

# Duplicate the slide and place it at the first position
requests = [
    {
        'duplicateObject': {
            'objectId': slide_id,
            'objectIds': {},
        }
    }
]

# Execute the batch update request
response = slides_service.presentations().batchUpdate(presentationId=presentation_id, body={'requests': requests}).execute()

# Get the ID of the duplicated slide
duplicated_slide_id = response['replies'][0]['duplicateObject']['objectId']

print(f'Slide duplicated successfully! Duplicated slide ID: https://docs.google.com/presentation/d/{presentation_id}/edit#slide=id.{duplicated_slide_id}')
```
