<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Create_draft_email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Create+draft+email:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #email #draft #create #python #library

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will show how to create a draft email using the Gmail API. It is usefull for organizations that need to automate the creation of emails.

**References:**
- [Gmail API Documentation](https://developers.google.com/gmail/api/quickstart/python)
- [Gmail API Python Quickstart](https://developers.google.com/gmail/api/quickstart/python)

## Input

### Import libraries


```python
import naas
from googleapiclient.discovery import build
from google_auth_oauthlib.flow import InstalledAppFlow
from google.auth.transport.requests import Request
import pickle
import datetime
import os.path
import base64
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
```

### Setup Variables
- `client_secret_file`: This variable stores the file path to the client secret file for Gmail API authentication.
- `api_name`: This variable stores the name or identifier of the Gmail API.
- `api_version`: This variable stores the version of the Gmail API.
- `scopes`: This variable stores the required scopes for accessing Gmail API.
- `email_from`: This variable stores the email address of the sender.
- `email_to`: This variable stores the email addresses of the recipients.
- `email_cc`: This variable stores the email addresses of the CC recipients.
- `email_subject`: This variable stores the subject of the email.
- `email_body`: This variable stores the body or content of the email.

For more information on how to setup the credentials, please refer to the [Gmail API Python Quickstart](https://developers.google.com/gmail/api/quickstart/python).


```python
# Inputs
client_secret_file = "./secrets-gmail.json"
api_name ='gmail'
api_version = 'v1'
scopes = ['https://mail.google.com/']

# Outputs
email_from = ""
email_to = ""
email_cc = ""
email_subject = 'Hello Gmail API'
email_body = 'Hello!! You work super cool!!'
```

## Model

### Connect to service


```python
# Create service account
def Create_Service(client_secret_file, api_name, api_version, *scopes):
    # Init variables
    print(client_secret_file, api_name, api_version, scopes, sep='-')
    CLIENT_SECRET_FILE = client_secret_file
    API_SERVICE_NAME = api_name
    API_VERSION = api_version
    SCOPES = [scope for scope in scopes[0]]
    print(SCOPES)
    cred = None
    
    # Create pickle file
    pickle_file = f'token_{API_SERVICE_NAME}_{API_VERSION}.pickle'
    if os.path.exists(pickle_file):
        with open(pickle_file, 'rb') as token:
            cred = pickle.load(token)

    if not cred or not cred.valid:
        if cred and cred.expired and cred.refresh_token:
            cred.refresh(Request())
        else:
            flow = InstalledAppFlow.from_client_secrets_file(CLIENT_SECRET_FILE, SCOPES)
            cred = flow.run_local_server()

        with open(pickle_file, 'wb') as token:
            pickle.dump(cred, token)

    try:
        service = build(API_SERVICE_NAME, API_VERSION, credentials=cred)
        print(API_SERVICE_NAME, 'service created successfully')
        return service
    except Exception as e:
        print('Unable to connect.')
        print(e)
        return None
    
service = Create_Service(client_secret_file, api_name, api_version, scopes)
```

## Output

### Create draft email

This function will create a draft email using the Gmail API.


```python
mimeMessage = MIMEMultipart()
mimeMessage['from'] = email_from
mimeMessage['to'] = email_to
mimeMessage['cc'] = email_cc
mimeMessage['subject'] = email_subject
mimeMessage.attach(MIMEText(email_body, 'plain'))
raw_string = base64.urlsafe_b64encode(mimeMessage.as_bytes()).decode()
response = service.users().drafts().create(
    userId='me',
    body={'message': {'raw': raw_string }}
).execute()

# Display result
print(response)
```

 
