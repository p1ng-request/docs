<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_List_slides_in_presentation.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+List+slides+in+presentation:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googleslides #presentation #list #slides #python #api

**Author:** [Florent Ravenel](https://linkedin.com/in/florent-ravenel)

**Description:** This notebook will list all the slides in a Google Slides presentation and is usefull for organizations that need to quickly access the content of a presentation.

**References:**
- [Google Slides API Documentation](https://developers.google.com/slides/how-tos/overview)
- [Google Slides API Python Quickstart](https://developers.google.com/slides/quickstart/python)

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
- `presentation_url`: The URL of the presentation to add the slide to.


```python
# Inputs
secret_path = 'secret.json'
scopes = [
    'https://www.googleapis.com/auth/presentations',
    'https://www.googleapis.com/auth/presentations.readonly'
]
presentation_url = "https://docs.google.com/presentation/d/xxxxxxxxxxxxxxxxx/"
```

## Model

### Connect to client


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
slides_service = build('slides', 'v1', credentials=credentials)
```

### Get presentation


```python
# Get the presentation ID from URL
presentation_id = presentation_url.split("/d/")[-1].split("/")[0]

# Call the presentations().get method to get the details of the presentation
presentation = slides_service.presentations().get(presentationId=presentation_id).execute()

# Extract the details of the presentation from the response
presentation_title = presentation.get('title')
presentation_page_size = presentation.get('pageSize')

# Print the details of the presentation
print(f'Presentation ID: {presentation_id}')
print(f'Title: {presentation_title}')
```

## Output

### List slides


```python
# Call the slides().list() method to retrieve the slides in the presentation
slides = slides_service.presentations().get(presentationId=presentation_id).execute()
list_slides = slides.get("slides")
print("Slides fetched:", len(list_slides))
list_slides[0]
```
