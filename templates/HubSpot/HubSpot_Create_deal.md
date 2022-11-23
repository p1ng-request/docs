<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Create_deal.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Create+deal:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #deal #naas_drivers #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description :** This notebook create a deal in HubSpot.

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

#### Enter deal parameters


```python
dealname = "TEST"
closedate = None #must be in format %Y-%m-%d
amount = None
hubspot_owner_id = None
```

#### Enter deal stage ID


```python
df_pipelines = hubspot.connect(HS_ACCESS_TOKEN).pipelines.get_all()
df_pipelines
```


```python
dealstage = '5102584'
```

## Model

### Create deal using send method
This method will allow you to add any deal properties available in your HubSpot.


```python
deal1 = {"properties": 
                  {
                    "dealstage": dealstage,
                    "dealname": dealname,
                    "amount": amount,
                    "closedate": closedate,
                    "hubspot_owner_id": hubspot_owner_id,
                   }
                 }

deal1 = hubspot.connect(HS_ACCESS_TOKEN).deals.send(send_deal)
```

### Create deal using create method


```python
deal2 = hubspot.connect(HS_ACCESS_TOKEN).deals.create(
    dealname,
    dealstage,
    closedate
)
```

## Output

### Display results


```python
deal1
```


```python
deal2
```
