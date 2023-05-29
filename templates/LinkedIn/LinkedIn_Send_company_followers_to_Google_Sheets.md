<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Send_company_followers_to_Google_Sheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Send+company+followers+to+Google+Sheets:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #company #followers #naas_drivers #automation #googlesheets #content

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to export their LinkedIn company followers to a Google Sheets spreadsheet.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import libraries


```python
from naas_drivers import linkedin, gsheet
import pandas as pd
import naas
```

### Setup LinkedIn
👉 <a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
# Credentials
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585

# Company URL
COMPANY_URL = "https://www.linkedin.com/company/naas-ai/"
```

### Setup Google Sheets
Share your spreadsheet with 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com 


```python
# Enter spreadsheet URL and sheet name
SPREADSHEET_URL = "https://docs.google.com/spreadsheets/d/1SoF6qIOeAKStOIx9FrMhcElN7XuiKiqPutZy823BgsY/edit#gid=0"
SHEET_NAME = "NAAS_FOLLOWERS"
```

### Setup Naas


```python
# Schedule your notebook everyday at 9:00 AM
naas.scheduler.add(cron="0 9 * * *")

# -> Uncomment the line below to remove your scheduler
# naas.scheduler.delete()
```

## Model

### Get followers from company
**Available columns :**
- FIRSTNAME : First name
- LASTNAME : Last name
- OCCUPATION : Text below the name in the profile page
- PROFILE_PICTURE : Profile picture URL
- PROFILE_URL : Profile URL
- PROFILE_ID : LinkedIn profile id
- PUBLIC_ID : LinkedIn public profile id
- FOLLOWED_AT : Date of following company
- DISTANCE : Distance between your profile


```python
df_gsheet = gsheet.connect(SPREADSHEET_URL).get(SHEET_NAME)
df_gsheet
```


```python
def get_new_followers(df):
    # Get all profiles
    profiles = []
    if len(df) > 0:
        profiles = df.PROFILE_ID.unique()
    start = 0
    while True:
        tmp_df = linkedin.connect(LI_AT, JSESSIONID).company.get_followers(
            COMPANY_URL, start=start, limit=1, sleep=False
        )
        profile_id = None
        if "PROFILE_ID" in tmp_df.columns:
            profile_id = tmp_df.loc[0, "PROFILE_ID"]
        if profile_id in profiles:
            break
        else:
            df = pd.concat([tmp_df, df])
            start += 1
    return df.reset_index(drop=True)


df_followers = get_new_followers(df_gsheet)
df_followers
```

## Output

### Save data in spreadsheet


```python
gsheet.connect(SPREADSHEET_URL).send(
    data=df_followers, sheet_name=SHEET_NAME, append=False
)
```


```python

```
