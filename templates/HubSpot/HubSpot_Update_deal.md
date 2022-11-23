<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_deal.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Update+deal:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #deal #naas_drivers #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description :** This notebook update a deal in HubSpot.

## Input

### Import libraries


```python
from naas_drivers import hubspot
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

#### Enter Your Access Token


```python
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Enter deal parameters to update


```python
deal_id = "3501002068"
dealname = "TEST"
dealstage = '5102584'
closedate = '2021-12-31' #date format must be %Y-%m-%d
amount = '100.50'
hubspot_owner_id = None
```

## Model

### Update deal using patch method
This method will allow you to update any deal properties available in your HubSpot.


```python
update_deal = {"properties": 
                  {
                    "dealstage": dealstage,
                    "dealname": dealname,
                    "amount": amount,
                    "closedate": closedate,
                    "hubspot_owner_id": hubspot_owner_id,
                   }
                 }

deal1 = hubspot.connect(HS_ACCESS_TOKEN).deals.patch(deal_id,
                                                     update_deal)
```

### Update deal using update method


```python
deal2 = hubspot.connect(HS_ACCESS_TOKEN).deals.update(
    deal_id,
    dealname,
    dealstage,
    closedate,
    amount,
    hubspot_owner_id
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
