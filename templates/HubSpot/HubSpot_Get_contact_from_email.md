<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_contact_from_email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Get+contact+from+email:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows you to extract contact information from emails sent through HubSpot.

## Input

### Import libraries


```python
from naas_drivers import hubspot
import naas
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

#### Enter Your Access Token


```python
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Enter your contact email


```python
contact_email = "ENTER_CONTACT_EMAIL_HERE"  # EXAMPLE : "email@gmail.com"
```

#### Enter your Contact properties
List of properties you want to get from contact.<br>
By default, you will get: 
- email
- firstname
- lastname
- createdate
- lastmodifieddate
- hs_object_id


```python
properties = []
```

## Model

### Get single contact


```python
contact = hubspot.connect(HS_ACCESS_TOKEN).contacts.get(
    contact_email, properties, idproperty="email"
)
```

## Output

### Display result


```python
contact
```
