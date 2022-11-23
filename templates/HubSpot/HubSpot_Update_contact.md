<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_contact.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Update+contact:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description :** This notebook update a contact in HubSpot.

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

#### Enter contact parameters to update


```python
contact_id = "280751"
email = "test@cashstory.com"
firstname = "Jean test"
lastname ='CASHSTOrY'
phone = "+336.00.00.00.00"
jobtitle = "Consultant"
website = "www.cashstory.com"
company = 'CASHSTORY'
hubspot_owner_id = None
```

## Model

### Update contact using send method
This method will allow you to add any contact properties available in your HubSpot.


```python
update_contact = {"properties": 
                  {
                    "email": email,
                    "firstname": firstname,
                    "lastname": lastname,
                    "phone": phone,
                    "jobtitle": jobtitle,
                    "website": website,
                    "company": company,
                    "url": "test3",
                    "hubspot_owner_id": hubspot_owner_id,
                   }
                 }

contact_id1 = hubspot.connect(HS_ACCESS_TOKEN).contacts.patch(
    contact_id,
    update_contact
)
```

### Update contact using update method


```python
contact_id2 = hubspot.connect(HS_ACCESS_TOKEN).contacts.update(
    contact_id,
    email,
    firstname,
    lastname,
    phone,
    jobtitle,
    website,
    company,
    hubspot_owner_id
)
```

## Output

### Display results


```python
contact_id1
```


```python
contact_id2
```
