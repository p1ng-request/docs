    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Calendar/Google_Calendar_List_events_from_calendar.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Calendar+-+List+events+from+calendar:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googlecalendar #calendar #events #list #api #python

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil)

**Description:** This notebook will demonstrate how to use the Google Calendar API to list events from a calendar.

**References:**
- [Google Calendar API Reference](https://developers.google.com/calendar/api/v3/reference/events/list)
- [Google Calendar API Python Quickstart](https://developers.google.com/calendar/quickstart/python)

## Input

### Import libraries


```python
from pprint import pprint
from datetime import datetime
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
- `time_min`: min time to start getting events from (example: '2023-04-11T14:44:29.977036Z')
- `max_results`: number of events to be returned
Assuming you have got the credentials, you can proceed further.


```python
# Inputs
scopes = ['https://www.googleapis.com/auth/calendar']
secret_path = "secrets.json"
calendar_id = "primary"
time_min = datetime.utcnow().isoformat() + 'Z'
max_results = 10
```

### Connect to service
Connect to service and copy/paste the autorization code in the input box below


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
service = build("calendar", "v3", credentials=credentials)
```

## Model

### List Events

List events from the specified calendar.


```python
print(f'Getting the upcoming {max_results} events')
events_result = service.events().list(
    calendarId=calendar_id,
    timeMin=time_min,
    maxResults=max_results,
    singleEvents=True,
    orderBy='startTime'
).execute()
events = events_result.get('items', [])

if not events:
    print('No upcoming events found😢')
```

## Output

### Display result


```python
for event in events:
    start = event['start'].get('dateTime', event['start'].get('date'))
    print(start, event['summary'])
```

 
