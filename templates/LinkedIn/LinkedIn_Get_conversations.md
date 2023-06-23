# Get conversations

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_conversations.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+conversations:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #message #getconversations #naas\_drivers #content #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides guidance on how to use LinkedIn to start meaningful conversations with potential connections.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
```

#### Get your cookies

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585
```

### Model

```python
df = linkedin.connect(LI_AT, JSESSIONID).message.get_conversations()
```

Get the information return in a dataframe.\
\
**Available columns :**

* CONVERSATION\_URN
* PARTICIPANTS : Urn of the participants
* LAST\_ACTIVITY
* IS\_GROUP\_CHAT
* GROUP\_CHAT\_NAME
* FOLLOWER\_COUNT
* IS\_PRIVATE\_CHAT
* PROFILE\_URN
* PROFILE\_ID
* FIRSTNAME
* LASTNAME
* OCCUPATION
* MESSAGE\_URN
* SENDER\_URN
* CREATED\_AT
* MESSAGE\_BODY

### Output

#### Display result

```python
df
```
