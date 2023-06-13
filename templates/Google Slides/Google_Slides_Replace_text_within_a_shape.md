<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Slides/Google_Slides_Replace_text_within_a_shape.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Slides+-+Replace+text+within+a+shape:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googleslides #text #shape #replace #api #slides

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to use the Slides API to modify the text content of a shape establishing a seamless connection using OAuth consent.

**References:**
- [Google Slides API](https://developers.google.com/slides/api/guides/styling)
- [Google Slides API Documentation](https://developers.google.com/slides/how-tos/overview)

## Input

### Import libraries


```python
try:
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
    from googleapiclient.errors import HttpError
except ModuleNotFoundError:
    !pip install google-api-python-client
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
    from googleapiclient.errors import HttpError
```

### Setup Variables
- `secret_path`: Set the path to the credentials JSON file
- `scopes`: Set the scopes required for accessing Google Slides
- `presentation_url`: The URL of the presentation to add the slide to.
- `shape_id`: ID of the shape to be modified. To get it, get the "pageElements" of your slide and find the objectId desired
- `replacement_text`: Text to be replaced


```python
# Inputs
secret_path = 'secret.json'
scopes = ['https://www.googleapis.com/auth/presentations', 'https://www.googleapis.com/auth/presentations.readonly']
presentation_url = "https://docs.google.com/presentation/d/xxxxxx/"
shape_id = "SLIDES_API583292764_2"
replacement_text = "TOOL - ACTION OF THE TOOL"
```

## Model

### Connect to client


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
slides_service = build('slides', 'v1', credentials=credentials)
```

## Output

### Replace text within a shape
The Slides API lets you modify the text content of a shape. You can remove individual ranges of text, and you can insert text at a specific location.


```python
def simple_text_replace(
    slides_service,
    presentation_url,
    shape_id,
    replacement_text
):
    # Get the presentation ID from URL
    presentation_id = presentation_url.split("/d/")[-1].split("/")[0]

    # pylint: disable=maybe-no-member
    try:
        # Remove existing text in the shape, then insert new text.
        requests = []
        requests.append({
            'deleteText': {
                'objectId': shape_id,
                'textRange': {
                    'type': 'ALL'
                }
            }
        })
        requests.append({
            'insertText': {
                'objectId': shape_id,
                'insertionIndex': 0,
                'text': replacement_text
            }
        })

        # Execute the requests.
        body = {
            'requests': requests
        }
        response = slides_service.presentations().batchUpdate(
            presentationId=presentation_id, body=body).execute()
        print(f"Replaced text in shape with ID: {shape_id}")
        return response
    except HttpError as error:
        print(f"An error occurred: {error}")
        print("Text is not merged")
        return error
    
# Put the slides_service, presentation_id, shape_id and replacement_text
res = simple_text_replace(
    slides_service,
    presentation_url,
    shape_id,
    replacement_text
)
```
