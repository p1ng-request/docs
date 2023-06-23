# Get invitations received

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_invitations\_received.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+invitations+received:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #content #operations #snippet #invitation #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E\_TXYWitQkmwog/)

**Description:** This notebook provides an overview of invitations received on LinkedIn.

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

* PROFILE\_ID : Sender LinkedIn unique profile id
* PROFILE\_URL : Sender LinkedIn profile URL
* PUBLIC\_ID : Sender LinkedIn public profile id
* FIRSTNAME : Sender first name
* LASTNAME : Sender last name
* FULLNAME : Sender first and last name
* OCCUPATION : Sender occupation
* PROFILE\_PICTURE : Sender profile picture
* MESSAGE : Message sent with the invitation
* SENT\_AT : Date time the invitation was sent at (Only for "Profile" invitation)
* UNSEEN : Boolean to know if the invitation have already been seen (Boolean: True or False)
* INVITATION\_TYPE : Type of invitation. It could be "Profile", "Company", "Event", "Newsletter"
* INVITATION\_DESC : Detailed type of invitation.
* INVITATION\_STATUS : Status of the invitation ("PENDING" for invitation from Profile)
* INVITATION\_ID : Secret to be used to accept or ignore invitation
* SHARED\_SECRET : Secret to be used to accept or ignore invitation

```python
df_invitation = linkedin.connect(LI_AT, JSESSIONID).invitation.get_received()
```

### Output

#### Display result

```python
df_invitation
```

```python
```
