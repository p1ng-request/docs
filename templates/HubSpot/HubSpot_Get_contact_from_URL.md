<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_contact_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Get+contact+from+URL:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description :** This notebook get a contact from HubSpot using its URL. Data will be returned as json with keys: 
- 'id': number,
- 'properties': dict
- 'createdAt': datetime
- 'updatedAt': datetime
- 'archived': boolean

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

#### Enter your Contact URL


```python
contact_url =  "ENTER_CONTACT_URL_HERE" # EXAMPLE : "https://app.hubspot.com/contacts/0000011/contact/00001"
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

### Split contact URL to get contact ID


```python
contact_id = contact_url.split("/contact/")[-1]
```

### Get single contact


```python
contact = hubspot.connect(HS_ACCESS_TOKEN).contacts.get(contact_id)
```

## Output

### Display result


```python
contact
```
