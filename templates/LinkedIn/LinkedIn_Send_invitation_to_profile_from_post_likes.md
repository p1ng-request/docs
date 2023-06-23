# Send invitation to profile from post likes

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_invitation\_to\_profile\_from\_post\_likes.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+invitation+to+profile+from+post+likes:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #post #likes #naas\_drivers #invitation #content #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to send LinkedIn invitations to profiles based on post likes.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import pandas as pd
import naas
import time
```

#### Setup LinkedIn

👉 [How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
# Credentials
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585

# Post url
POST_URL = "POST_URL"
```

#### Setup Outputs

```python
# Post likes
csv_post_likes = (
    f"LINKEDIN_POST_LIKES_{POST_URL.split('activity-')[1].split('-')[0]}.csv"
)
```

### Model

#### Get likes from post

```python
df_post_likes = linkedin.connect(LI_AT, JSESSIONID).post.get_likes(POST_URL)
print("👍 Post likes :", len(df_post_likes))
df_post_likes.tail(1)
```

#### Get connections from post likes

```python
def get_connections(df):
    for index, row in df.iterrows():
        df_network = pd.DataFrame()
        profile = row["PUBLIC_ID"]
        print(f"➡️ Checking :", profile)

        # Get distance with profile
        if profile != 0:
            df_network = linkedin.connect(LI_AT, JSESSIONID).profile.get_network(
                profile
            )

        # Check if profile is already in your network
        if len(df_network) > 0:
            distance = df_network.loc[0, "DISTANCE"]
            df.loc[index, "DISTANCE"] = distance
            df.to_csv(csv_post_likes, index=False)
    return df


df_profile = get_connections(df_post_likes)
df_profile
```

### Output

#### Send invitations to profile out of network

```python
def send_invitation(df):
    df = df[~df.DISTANCE.isin(["SELF", "DISTANCE_1"])].reset_index(drop=True)
    for index, row in df.iterrows():
        fullname = row["FULLNAME"]
        profile_id = row["PROFILE_ID"]
        print(f"➡️ Sending to :", fullname)

        # Get distance with profile
        try:
            linkedin.invitation.send(recipient_url=profile_id)
        except Exception as e:
            print("❌ Invitation not sent", e)
        time.sleep(3)
    return df


df_invitation = send_invitation(df_profile)
df_invitation
```
