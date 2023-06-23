# Send comments from post to gsheet

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_comments\_from\_post\_to\_gsheet.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+comments+from+post+to+gsheet:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #post #comments #gsheet #naas\_drivers #content #snippet #googlesheets

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to automatically send comments from a LinkedIn post to a Google Sheet.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin, gsheet
import random
import time
import pandas as pd
from datetime import datetime
```

#### Setup LinkedIn

👉 [How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"

# Post url
POST_URL = "POST_URL"
```

#### Setup your Google Sheet

👉 Get your spreadsheet id => it is located in your gsheet url after "https://docs.google.com/spreadsheets/d/" and before "/edit"\
👉 Share your gsheet with our service account to connect : naas-share@naas-gsheets.iam.gserviceaccount.com\
👉 Create your sheet before sending data into it

```python
# Spreadsheet id
SPREADSHEET_ID = "SPREADSHEET_ID"

# Sheet names
SHEET_POST_COMMENTS = "POST_COMMENTS"
SHEET_MY_NETWORK = "MY_NETWORK"
SHEET_NOT_MY_NETWORK = "NOT_MY_NETWORK"
```

#### Constant

```python
DATETIME_FORMAT = "%Y-%m-%d %H:%M:%S"
```

### Model

#### Get likes from post

```python
df_posts = linkedin.connect(LI_AT, JSESSIONID).post.get_comments(POST_URL)
df_posts["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
```

#### Get network for profiles

```python
df_network = pd.DataFrame()

for _, row in df_posts.iterrows():
    profile_id = row.PROFILE_ID
    # Get network information to know distance between you and people who likes the post
    tmp_network = linkedin.connect(LI_AT, JSESSIONID).profile.get_network(profile_id)
    # Concat dataframe
    df_network = pd.concat([df_network, tmp_network], axis=0)
    # Time sleep in made to mimic human behavior, here it is randomly done between 2 and 5 seconds
    time.sleep(random.randint(2, 5))

df_network.head(5)
```

#### Merge posts likes and network data

```python
df_all = pd.merge(df_posts, df_network, on=["PROFILE_URN", "PROFILE_ID"], how="left")
df_all = df_all.sort_values(by=["FOLLOWERS_COUNT"], ascending=False)
df_all = df_all[df_all["DISTANCE"] != "SELF"].reset_index(drop=True)
df_all.head(5)
```

#### Split my network or not

```python
# My network
my_network = df_all[df_all["DISTANCE"] == "DISTANCE_1"].reset_index(drop=True)
my_network["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
my_network.head(5)
```

```python
# Not in my network
not_my_network = df_all[df_all["DISTANCE"] != "DISTANCE_1"].reset_index(drop=True)
not_my_network["DATE_EXTRACT"] = datetime.now().strftime(DATETIME_FORMAT)
not_my_network.head(5)
```

### Output

#### Save post comments in gsheet

```python
gsheet.connect(SPREADSHEET_ID).send(
    df_posts, sheet_name=SHEET_POST_COMMENTS, append=False
)
```

#### Save people from my network in gsheet

```python
gsheet.connect(SPREADSHEET_ID).send(
    my_network, sheet_name=SHEET_MY_NETWORK, append=False
)
```

#### Save people not in my network in gsheet

```python
gsheet.connect(SPREADSHEET_ID).send(
    not_my_network, sheet_name=SHEET_NOT_MY_NETWORK, append=False
)
```
