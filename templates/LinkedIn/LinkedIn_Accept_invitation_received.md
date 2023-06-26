<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Accept_invitation_received.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Accept+invitation+received:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #content #operations #snippet #invitation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook allows you to accept invitations to connect on LinkedIn.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import libraries



```python
from naas_drivers import linkedin
import pandas as pd
```

### Setup LinkedIn

- [Get your cookies](/d20a8e7e508e42af8a5b52e33f3dba75)


```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"
```

### Get invitations


```python
df_invitation = linkedin.connect(LI_AT, JSESSIONID).invitation.get_received()
df_invitation
```

### Setup invitation id and shared secret


```python
# Value in column "INVITATION_ID"
invitation_id = "691596420000000000"

# Value in column "SHARED_SECRET"
shared_secret = "6xubdsfs"

# If "INVITATION_TYPE" is "Profile" then False else True
is_generic = False
```

## Model

### Accept invitation received


```python
result = linkedin.connect(LI_AT, JSESSIONID).invitation.accept(
    invitation_id, shared_secret, is_generic
)
```

## Output


### Display result


```python
result
```
