# Get invitations sent

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_invitations\_sent.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+invitations+sent:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #content #operations #snippet #invitation #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E\_TXYWitQkmwog/)

**Description:** This notebook helps you to send invitations to connect on LinkedIn.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import pandas as pd
```

#### Setup LinkedIn

* [Get your cookies](../../d20a8e7e508e42af8a5b52e33f3dba75/)

```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"
```

### Model

#### Get invitations

Get the information returned in a dataframe.\
\
**Available columns :**

* PROFILE\_ID : Receiver LinkedIn unique profile id
* PROFILE\_URL : Receiver LinkedIn profile URL
* PUBLIC\_ID : Receiver LinkedIn public profile id
* FIRSTNAME : Receiver first name
* LASTNAME : Receiver last name
* FULLNAME : Receiver first and last name
* OCCUPATION : Receiver occupation
* PROFILE\_PICTURE : Receiver profile picture
* MESSAGE : Message sent with the invitation
* SENT\_AT : Date time the invitation was sent at (Only for "Profile" invitation)
* INVITATION\_TYPE : Type of invitation. It could be "Profile", "Company", "Event", "Newsletter"
* INVITATION\_DESC : Detailed type of invitation.
* INVITATION\_STATUS : Status of the invitation ("PENDING" for invitation from Profile)
* INVITATION\_ID : Secret to be used to accept or ignore invitation

```python
df_invitation = linkedin.connect(LI_AT, JSESSIONID).invitation.get_sent()
```

### Output

#### Display result

```python
df_invitation
```
