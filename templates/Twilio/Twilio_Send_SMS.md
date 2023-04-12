<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twilio/Twilio_Send_SMS.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twilio+-+Send+SMS:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #twilio #project #send #sms #snippet #operations #dataframe

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook allows you to send SMS messages using the Twilio API.

## Input

## Import Library


```python
try:
    from twilio.rest import Client
except:
    ! pip install --user twilio
    from twilio.rest import Client
```

### Setup Twilio
- [Get your credentials](https://support.twilio.com/hc/en-us/articles/223136027-Auth-Tokens-and-How-to-Change-Them)


```python
# Credentials
account_sid = ""  # From Twilio Console
auth_token = ""  # From Twilio Console

# Message
from_number = (
    ""  # Buy a new number if not available preferably starting with "+1" country code
)
to_number = ""  # Could send messages only to verified Caller ID's
message = ""  # Message to be Sent
```

## Model


### Set Client


```python
client = Client(account_sid, auth_token)  # Set Client
```

## Output


### Send message


```python
client.api.account.messages.create(to=to_number, from_=from_number, body=message)
```
