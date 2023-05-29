<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Send_followers_demographic_data_to_a_Google_Sheets_spreadsheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Send+followers+demographic+data+to+a+Google+Sheets+spreadsheet:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** "linkedin #googlesheets #gsheet #data #naas_drivers #demographics #content #snippet

**Author:** [Asif Syed](https://www.linkedin.com/in/asifsyd/)

**Description:** This notebook allows users to easily export demographic data about their LinkedIn followers to a Google Sheets spreadsheet.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import library


```python
from naas_drivers import gsheet
from naas_drivers import linkedin
import pandas as pd
import numpy as np
import naas
```

### Setup LinkedIn
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
# LinkedIn cookies
LI_AT = (
    naas.secret.get("LI_AT") or "ENTER_YOUR_COOKIE_HERE"
)  # EXAMPLE : "AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2"
JSESSIONID = (
    naas.secret.get("JSESSIONID") or "ENTER_YOUR_JSESSIONID_HERE"
)  # EXAMPLE : "ajax:8379907400220387585"
```

### Setup Google Sheets
Share your spreadsheet with 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com


```python
SPREADSHEET_URL = "ENTER_YOUR_SPREADSHEET_URL_HERE"
SHEET_NAME = "ENTER_YOUR_SHEET_NAME_HERE"
```

## Model

### Connect to LinkedIn


```python
linkedin.connect(LI_AT, JSESSIONID)
```

### Connect to gsheet


```python
gsheet.connect(SPREADSHEET_URL)
```

### Get the profiles of last 'n' followers (n is the value assigned to limit parameter below)

The 'start' parameter below specifies the number of initial rows to be skipped. 

These initial rows refer to the most recent profiles, hence it is by default maintained as 0, but it could be customized as per the need. 


```python
df = linkedin.network.get_followers(start=0, limit=1)
profiles = df["PROFILE_URL"]
```

### Get Industry name and country details for each profile


```python
df_identity = pd.DataFrame()
df1 = pd.DataFrame()
for counter, profile in enumerate(profiles):
    df1 = linkedin.profile.get_identity(profile_url=profile).loc[
        :, ["PROFILE_ID", "COUNTRY", "INDUSTRY_NAME"]
    ]
    df_identity = df_identity.append(df1)
```

### Get work experience details for each profile


```python
df_resume = pd.DataFrame()
df1 = pd.DataFrame()
for counter, profile in enumerate(profiles):
    df1 = linkedin.profile.get_resume(profile_url=profile)
    df_resume = df_resume.append(df1)
df_resume = df_resume[df_resume["CATEGORY"] == "Experience"].loc[
    :, ["PROFILE_ID", "TITLE", "DATE_START", "DATE_END", "PLACE", "FIELD"]
]
```

### Merge two data frames.


```python
df_final = pd.merge(df_identity, df_resume, how="inner", on="PROFILE_ID")
df_final
```

## Output

### Send the data


```python
gsheet.send(sheet_name=SHEET_NAME, data=df_final)
```
