<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Send_posts_feed_to_gsheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Send+posts+feed+to+gsheet:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #profile #post #stats #naas_drivers #automation #content #googlesheets

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook automates the process of sending LinkedIn posts to a Google Sheet for easy tracking and analysis.


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
import naas
import pandas as pd
```

### Setup LinkedIn
👉 <a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"

# Linkedin profile url
PROFILE_URL = "https://www.linkedin.com/in/xxxxxx/"

# Number of posts updated in Gsheet (This avoid to requests the entire database)
LIMIT = 10
```

### Setup your Google Sheet
👉 Get your spreadsheet URL<br>
👉 Share your gsheet with our service account to connect : naas-share@naas-gsheets.iam.gserviceaccount.com<br>
👉 Create your sheet before sending data into it


```python
# Spreadsheet URL
SPREADSHEET_URL = "https://docs.google.com/spreadsheets/d/XXXXXXXXXXXXXXXXXXXX"

# Sheet name
SHEET_NAME = "LK_POSTS_FEED"
```

### Setup Naas


```python
naas.scheduler.add(cron="0 8 * * *")

# -> To delete your scheduler, please uncomment the line below and execute this cell
# naas.scheduler.delete()
```

## Model

### Get data from Google Sheet


```python
df_gsheet = gsheet.connect(SPREADSHEET_URL).get(sheet_name=SHEET_NAME)
df_gsheet
```

### Get new posts and update last posts stats


```python
def get_new_posts(df_gsheet, key, limit=LIMIT, sleep=False):
    posts = []
    if len(df_gsheet) > 0:
        posts = df_gsheet[key].unique()
    else:
        df_posts_feed = linkedin.connect(LI_AT, JSESSIONID).profile.get_posts_feed(
            PROFILE_URL, limit=-1, sleep=sleep
        )
        return df_posts_feed

    # Get new
    df_posts_feed = linkedin.connect(LI_AT, JSESSIONID).profile.get_posts_feed(
        PROFILE_URL, limit=LIMIT, sleep=sleep
    )
    df_new = pd.concat([df_posts_feed, df_gsheet]).drop_duplicates(key, keep="first")
    return df_new


df_new = get_new_posts(df_gsheet, "POST_URL", limit=LIMIT)
df_new
```

## Output

### Send to Google Sheet


```python
gsheet.connect(SPREADSHEET_URL).send(df_new, sheet_name=SHEET_NAME, append=False)
```
