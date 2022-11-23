<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Send_deals_to_gsheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Send+deals+to+gsheet:+Error+short+description">Bug report</a>

**Tags:** #hubspot #crm #sales #deal #naas_drivers #gsheet #snippet #googlesheets

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description :** This notebook send all your deals to a Google Sheets spreadsheet.

## Input

### Import libraries


```python
from naas_drivers import hubspot, gsheet
import naas
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

#### Enter Your Access Token


```python
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Enter your Deal properties
List of properties you want to get from deal.<br>
By default, you will get: 
- dealname
- amount
- dealstage
- pipeline
- createdate
- closedate
- hs_object_id
- hs_lastmodifieddate


```python
properties = []
```

### Setup your Google Sheets

Pre-requisite: share your Google Sheets with our service account: 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com


```python
SPREADSHEET_URL = "ENTER_YOUR_SPREADSHEET_URL_HERE"
SHEET_NAME = "ENTER_YOUR_SHEET_NAME_HERE"
```

## Model

### Get deals


```python
df_deals = hubspot.connect(HS_ACCESS_TOKEN).deals.get_all(properties)
```

## Output

### Send contacts to gsheet


```python
gsheet.connect(SPREADSHEET_URL).send(
    sheet_name=SHEET_NAME,
    data=df_deals,
    append=False
)
```
