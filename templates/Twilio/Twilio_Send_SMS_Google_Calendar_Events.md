<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twilio/Twilio_Send_SMS_Google_Calendar_Events.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twilio+-+Send++SMS+messages+for+Google+Calendar+Events:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googlecalendar #twilio #notification #event

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil)

**Description:** This notebook sends an SMS notification for upcoming the next event you're attending in your Google Calendar.

**References:**
- https://developers.google.com/calendar/api/quickstart/python

## Input

### Import libraries


```python
import naas
from datetime import datetime
import pytz
try:
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow
except ModuleNotFoundError:
    !pip install google-api-python-client --user
    from apiclient.discovery import build
    from google_auth_oauthlib.flow import InstalledAppFlow 
try:
    from twilio.rest import Client
except ModuleNotFoundError:
    !pip install twilio --user
    from twilio.rest import Client
import pickle
```

### Setup Variables

1. [Twilio](https://console.twilio.com)
- `account_sid`: Account SID
- `auth_token`: Authentication Token
- `twilio_phone_number`: My Twilio phone number
- `twilio_verified_phone_number`: Twilio verified phone number

2. [Google Cloud](https://console.cloud.google.com/)
Follow this [blog](https://blog.sriniketh.design/getting-credentials-from-gcp-google-cloud-platform) to know how to get the credentials from GCP
- `scopes`: The scopes to be used for authentication
- `secret_path`: secret json path extracted from GCP
Assuming you have got the credentials, you can proceed further.

Then you are all set to proceed further 🚀


```python
# Inputs
account_sid = naas.secret.get("TWILIO_ACCOUNT_SID")
auth_token = naas.secret.get("TWILIO_AUTH_TOKEN")
twilio_phone_number = naas.secret.get("TWILIO_FROM_NUMBER")
twilio_verified_phone_number = naas.secret.get("TWILIO_TO_NUMBER")
scopes = ['https://www.googleapis.com/auth/calendar']
secret_path = "secrets.json"
calendar_id = "primary"
time_min = datetime.utcnow().isoformat() + 'Z'
time_zone = 'Europe/Paris'
```

### Connect to service
Connect to service and copy/paste the autorization code in the input box below


```python
flow = InstalledAppFlow.from_client_secrets_file(secret_path, scopes=scopes)
credentials = flow.run_console()
service = build("calendar", "v3", credentials=credentials)
```

## Model

### Get next event


```python
events_result = service.events().list(
    calendarId=calendar_id,
    timeMin=time_min,
    maxResults=1,
    singleEvents=True,
    orderBy='startTime'
).execute()
events = events_result.get('items', [])
if not events:
    print('No upcoming events found😢')
    
# Parse datetime string
next_dt = datetime.fromisoformat(events[0].get("start").get("dateTime"))

# Get the current datetime with timezone information
now_with_timezone = datetime.now(pytz.timezone(time_zone))  # Replace 'Your/Timezone' with your desired timezone

message = f"""
Hi there,
Kindly reminder!
📆 Next event: {events[0].get('summary')}
⏰ Start at {next_dt}
"""
print(message)
```

### Send notifications of new calendar Events


```python
def send_sms_google_calendar_events(to_phone_number, message):
    # Send SMS using Twilio
    client = Client(account_sid, auth_token)
    sent_message = client.messages.create(
        from_=twilio_phone_number,
        to=twilio_verified_phone_number,
        body=message)
    print(sent_message)
```

## Output

### Save result in csv


```python
if (next_dt - now_with_timezone).total_seconds() < 3600:
    send_sms_google_calendar_events(to_phone_number=twilio_verified_phone_number, message=message)
    print('\n\nDone🚀')
```
