<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Calendar/Google_Calendar_Get_calendar.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Calendar+-+Get+calendar:+Error+short+description">Bug report</a>

**Tags:** #googlecalendar #calendar #get #api #reference #v3

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil)

**Description:** This notebook will demonstrate how to use the Google Calendar API to get metadata for a calendar.

**References:**
- [Google Calendar API Reference](https://developers.google.com/calendar/api/v3/reference/calendars/get)

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
- `calendar_id`: calendar ID in Google Calendar
Assuming you have got the credentials, you can proceed further.


```python
# Inputs
scopes = ['https://www.googleapis.com/auth/calendar']
secret_path = "secrets.json"
calendar_id = "primary"
```

### Connect to service
Connect to service and copy/paste the autorization code in the input box below


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
service = build("calendar", "v3", credentials=credentials)
```

## Model

### Get calendar

This function will use the Google Calendar API to get metadata for a calendar.


```python
def get_calendar(calendar_id):
    calendar = service.calendars().get(calendarId=calendar_id).execute()
    return calendar
```

## Output

### Display result


```python
calendar = get_calendar(calendar_id)
pprint(calendar)
```

 
