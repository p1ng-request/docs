<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_Create_a_blank_presentation.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+Create+a+blank+presentation:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #google #slides #presentation #create #blank #api

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook creates a blank presentation with a specified title using Google Slides API while connecting with oauth consent.

**References:**
- [Google Slides API](https://developers.google.com/slides/api/guides/presentations)
- [Google Slides API Quickstart](https://developers.google.com/slides/quickstart/python)

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
```

### Setup Variables
- `secret_path`: Set the path to the credentials JSON file
- `scopes`: Set the scopes required for accessing Google Slides
- `title`: Title of the presentation


```python
secret_path = 'secret.json'
scopes = [
    'https://www.googleapis.com/auth/presentations',
    'https://www.googleapis.com/auth/presentations.readonly'
]
title = 'New Presentation'
```

## Model

### Connect to client


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
slides_service = build('slides', 'v1', credentials=credentials)
```

## Output

### Create a blank presentation


```python
# Create a new Google Slides presentation
presentation = {
    'title': title
}
presentation = slides_service.presentations() \
    .create(body=presentation).execute()

# Retrieve the presentation ID
presentation_id = presentation.get('presentationId')

# Create a new slide in the presentation
requests = [
    {
        'createSlide': {
            'insertionIndex': '1',  # Insert the new slide as the first slide
            'slideLayoutReference': {
                'predefinedLayout': 'TITLE_AND_TWO_COLUMNS'  # Specify the layout for the new slide
            }
        }
    }
]
slides_service.presentations().batchUpdate(
    presentationId=presentation_id,
    body={'requests': requests}).execute()

print(f'Google Slide created with presentation ID: https://docs.google.com/presentation/d/{presentation_id}')
```

 
