# Send posts feed to gsheet

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_posts\_feed\_to\_gsheet.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+posts+feed+to+gsheet:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #profile #post #stats #naas\_drivers #automation #content #googlesheets

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook automates the process of sending LinkedIn posts to a Google Sheet for easy tracking and analysis.

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

# Linkedin profile url
PROFILE_URL = "https://www.linkedin.com/in/xxxxxx/"

# Number of posts updated in Gsheet (This avoid to requests the entire database)
LIMIT = 10
```

#### Setup your Google Sheet

👉 Get your spreadsheet URL\
👉 Share your gsheet with our service account to connect : naas-share@naas-gsheets.iam.gserviceaccount.com\
👉 Create your sheet before sending data into it

```python
# Spreadsheet URL
SPREADSHEET_URL = "https://docs.google.com/spreadsheets/d/XXXXXXXXXXXXXXXXXXXX"

# Sheet name
SHEET_NAME = "LK_POSTS_FEED"
```

#### Setup Naas

```python
naas.scheduler.add(cron="0 8 * * *")

# -> To delete your scheduler, please uncomment the line below and execute this cell
# naas.scheduler.delete()
```

### Model

#### Get data from Google Sheet

```python
df_gsheet = gsheet.connect(SPREADSHEET_URL).get(sheet_name=SHEET_NAME)
df_gsheet
```

#### Get new posts and update last posts stats

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

### Output

#### Send to Google Sheet

```python
gsheet.connect(SPREADSHEET_URL).send(df_new, sheet_name=SHEET_NAME, append=False)
```
