<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Calendar/Google_Calendar_List_calendars.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Calendar+-+List+calendars:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googlecalendar #calendarlist #list #api #python #reference

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil)

**Description:** This notebook will demonstrate how to use the Google Calendar API to list the calendars on the user's calendar list.

**References:**
- [Google Calendar API Reference](https://developers.google.com/calendar/api/v3/reference/calendarList/list)
- [Google Calendar API Python Quickstart](https://developers.google.com/calendar/quickstart/python)

## Input

### Import libraries


```python
from pprint import pprint
try:
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
except ModuleNotFoundError:
    !pip install google-api-python-client
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
```

### Setup Variables
Follow this [blog](https://blog.sriniketh.design/getting-credentials-from-gcp-google-cloud-platform) to know how to get the credentials from GCP
- `scopes`: The scopes to be used for authentication
- `secret_path`: secret json path extracted from GCP
Assuming you have got the credentials, you can proceed further.


```python
# Inputs
scopes = ['https://www.googleapis.com/auth/calendar']
secret_path = "secrets.json"
```

### Connect to service
Connect to service and copy/paste the autorization code in the input box below


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
service = build("calendar", "v3", credentials=credentials)
```

## Model

### List Calendars

This function will use the Google Calendar API to list the calendars on the user's calendar list.


```python
def list_calendars(service):    
    # Call the Calendar API
    results = service.calendarList().list().execute()
    return results
```

## Output

### Display result


```python
calendars = list_calendars(service)
print("📅 Calendars found:", len(calendars))
pprint(calendars)
```

 
