# Send invitations to post commenters

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_invitations\_to\_post\_commenters.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+invitations+to+post+commenters:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #post #comments #invitations #connections #naas\_drivers #content #snippet #dataframe

**Author:** [Asif Syed](https://www.linkedin.com/in/asifsyd/)

**Description:** This notebook allows users to quickly and easily send LinkedIn invitations to people who have commented on their posts.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import naas
import time
```

#### Setup LinkedIn

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = (
    naas.secret.get("LI_AT") or "ENTER_YOUR_COOKIE_LI_AT_HERE"
)  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = (
    naas.secret.get("JSESSIONID") or "ENTER_YOUR_COOKIE_JSESSIONID_HERE"
)  # EXAMPLE ajax:8379907400220387585
```

#### Enter post URL

To get the URL for a post, click on the three dots option to the right corner of that post on LinkedIn and select "copy link to post" option.

Replace the string 'URL' below with the actual URL

```python
POST_URL = "URL"
```

### Model

#### Get comments of the post

Running the below cell fetches the information related to all the comments of the post and stores the information in a dataframe

```python
df = linkedin.connect(LI_AT, JSESSIONID).post.get_comments(POST_URL)
```

#### Get profile URLs of all the commenters

```python
profiles = df["PROFILE_URL"]  # storing the profile URLs of all the commenters
```

#### Filter these profiles to include only people out of network

```python
filtered_profiles = []
for i in profiles:
    distance = linkedin.profile.get_network(profile_url=i)["DISTANCE"]
    if distance[0] != "DISTANCE_1":
        filtered_profiles.append(i)
    time.sleep(3)
```

### Output

#### Send invitations to all the commenters

```python
for i in filtered_profiles:  # looping through each commenter's profile URL
    linkedin.connect(LI_AT, JSESSIONID).invitation.send(
        recipient_url=i
    )  # send invitation
```
