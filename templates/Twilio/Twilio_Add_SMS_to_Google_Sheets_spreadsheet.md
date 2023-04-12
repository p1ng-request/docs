    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twilio/Twilio_Add_SMS_to_Google_Sheets_spreadsheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twilio+-+Add+SMS+to+Google+Sheets+spreadsheet:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #twilio #google #sheets #googlesheets #send

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook allows you to log all the messages sent through your Twilio Account into a Google Sheets document. Each new message will be added as a new row, along with the date, time, message ID, and message content. It's a convenient way to keep track of your Twilio activity and make sure you never miss an important message.

## Input

### Import libraries


```python
from datetime import datetime
import naas

try:
    import gspread
except ModuleNotFoundError:
    !pip install gspread
    import gspread

try:
    from oauth2client.service_account import ServiceAccountCredentials
except ModuleNotFoundError:
    !pip install oauth2client
    from oauth2client.service_account import ServiceAccountCredentials
    
try:
    from twilio.rest import Client
except ModuleNotFoundError:
    !pip install twilio
    from twilio.rest import Client
```

### Setup Variables

1. [Twilio](https://console.twilio.com)

- Account SID
- Authentication Token
- My Twilio phone number
- Twilio verified phone number

2. [Google Cloud](https://console.cloud.google.com/)

- Create a new free cloud project
- Go to `API & Services` and enable Google Drive and Sheets API
- Then navigate to `Credentials` and create a new service account and provide correct permission (like editor[preferred], viewer, etc.)
- Then download the `.json` file in the same directory of the the notebook
- Then create a new [google sheet](sheets.new) and give it a name
- Go to `.json` file saved earlier and copy the email address from it
- Click on `Share` button in the Google sheets and paste the copied email id.

Then you are all set to proceed further 🚀


```python
#inputs

# Twilio
account_sid = naas.secret.get("TWILIO_ACCOUNT_SID")
auth_token = naas.secret.get("TWILIO_AUTH_TOKEN")
twilio_phone_number = naas.secret.get("TWILIO_FROM_NUMBER")
twilio_verified_phone_number = naas.secret.get("TWILIO_TO_NUMBER")

# Set up Google Sheets credentials
scope = ['https://spreadsheets.google.com/feeds', 'https://www.googleapis.com/auth/drive']
creds = ServiceAccountCredentials.from_json_keyfile_name('credentials.json', scope)
client = gspread.authorize(creds)
sheet = client.open('naas-test').sheet1  # Replace with the name of your Google Sheets file

# General
content = 'Testing Naas + Google Sheets integration'
```

## Model

### Send SMS (using Twilio) & add the logs as new row inside Google sheets


```python
def send_sms_and_add_to_google_sheets(to_phone_number, message):
    # Send SMS using Twilio
    client = Client(account_sid, auth_token)
    sent_message = client.messages.create(
        from_=twilio_phone_number,
        to=twilio_verified_phone_number,
        body=message)
    
    # Add new row to Google Sheets
    row = [datetime.now().isoformat(), sent_message.sid, sent_message.body]
    sheet.append_row(row)

    print(sent_message)
```

## Output

### Run the function to log the results


```python
send_sms_and_add_to_google_sheets(to_phone_number=twilio_verified_phone_number, message=content)
print('\n\nDone.')
```


```python

```
