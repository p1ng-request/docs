<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Create_contact.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Create+contact:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to create contacts in HubSpot, enabling them to store and manage customer information.

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

#### Enter contact parameters


```python
email = "test@cashstory.com"
firstname = "Test"
lastname = "CASHSTORY"
phone = "+33600000000"
jobtitle = "Consultant"
website = "www.cashstory.com"
company = "CASHSTORY"
hubspot_owner_id = None
```

## Model

### Create contact using send method
This method will allow you to add any contact properties available in your HubSpot.


```python
create_contact = {
    "properties": {
        "email": email,
        "firstname": firstname,
        "lastname": lastname,
        "phone": phone,
        "jobtitle": jobtitle,
        "website": website,
        "company": company,
        "url": "test",
        "hubspot_owner_id": hubspot_owner_id,
    }
}

contact1 = hubspot.connect(HS_ACCESS_TOKEN).contacts.send(create_contact)
```

### Create contact using create method


```python
contact2 = hubspot.connect(HS_ACCESS_TOKEN).contacts.create(
    email, firstname, lastname, phone, jobtitle, website, company, hubspot_owner_id
)
```

## Output

### Display results


```python
contact1
```


```python
contact2
```
