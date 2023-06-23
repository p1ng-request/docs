# Send connections from network to gsheet

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_connections\_from\_network\_to\_gsheet.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+connections+from+network+to+gsheet:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #network #connections #naas\_drivers #csv #automation #content #googlesheets

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to export their LinkedIn connections to a Google Sheet for easy organization and tracking.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin, gsheet
import naas
import pandas as pd
```

#### Setup LinkedIn

👉 [How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"
```

#### Setup your Google Sheet

👉 Get your spreadsheet URL\
👉 Share your gsheet with our service account to connect : naas-share@naas-gsheets.iam.gserviceaccount.com\
👉 Create your sheet before sending data into it

```python
# Spreadsheet URL
SPREADSHEET_URL = "https://docs.google.com/spreadsheets/d/XXXXXXXXXXXXXXXXXXXX"

# Sheet name
SHEET_NAME = "LK_CONNECTIONS"
```

#### Setup Naas

```python
naas.scheduler.add(cron="0 8 * * *")

# -> To delete your scheduler, please uncomment the line below and execute this cell
# naas.scheduler.delete()
```

### Model

#### Get connections from Google Sheet

```python
df_gsheet = gsheet.connect(SPREADSHEET_URL).get(sheet_name=SHEET_NAME)
df_gsheet
```

#### Get new connections

```python
def get_new_connections(df_gsheet, key="PROFILE_URN"):
    profiles = []
    if len(df_gsheet) > 0:
        profiles = df_gsheet[key].unique()
    else:
        df = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(limit=-1)
        return df

    # Get new
    df_new = pd.DataFrame()
    update = True
    while update:
        start = 0
        df = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(
            start=start, count=100, limit=100
        )
        new_profiles = df[key].unique()
        for i, p in enumerate(new_profiles):
            if p in profiles:
                update = False
                df = df[:i]
                break
        start += 100
        df_new = pd.concat([df_new, df])
    return df_new


df_new = get_new_connections(df_gsheet, key="PROFILE_URN")
df_new
```

### Output

#### Send to Google Sheet

```python
gsheet.connect(SPREADSHEET_URL).send(df_new, sheet_name=SHEET_NAME, append=True)
```
