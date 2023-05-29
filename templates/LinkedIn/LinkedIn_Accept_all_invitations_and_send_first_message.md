<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Accept_all_invitations_and_send_first_message.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Accept+all+invitations+and+send+first+message:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #content #operations #automation #invitation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook helps you quickly and easily accept all LinkedIn invitations and send a personalized introductory message to each new connection.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import libraries



```python
import naas
from naas_drivers import linkedin
import pandas as pd
```

### Setup Variables
If you are using the Chrome Extension:
- [Install Naas Chrome Extension](https://chrome.google.com/webstore/detail/naas/cpkgfedlkfiknjpkmhcglmjiefnechpp?hl=fr&authuser=0)
- [Create a new token](https://app.naas.ai/hub/token)
- Copy/Paste your token in your extension
- Login/Logout your LinkedIn account
- Your secrets "LINKEDIN_LI_AT" and "LINKEDIN_JSESSIONID" will be added directly on your naas everytime you login and logout.

or <br>

If you are not using the Google Chrome Extension, [learn how to get your cookies on LinkedIn](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)
- `li_at`: Cookie used to authenticate Members and API clients
- `JSESSIONID`: Cookie used for Cross Site Request Forgery (CSRF) protection and URL signature validation
- `cron`: Cron params for naas scheduler. More information: https://crontab.guru/
- `first_message`: First message to be send


```python
# Inputs
li_at = naas.secret.get("LINKEDIN_LI_AT") or "YOUR_COOKIE_LI_AT"
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID") or "YOUR_COOKIE_JSESSIONID"
cron = "0 * * * *"

# Outputs
first_message = "Hello, Nice to connect!"
```

## Model

### Get invitations received


```python
df_invitation = linkedin.connect(li_at, JSESSIONID).invitation.get_received()
df_invitation
```

### Accept pending invitations received from "Profile"


```python
def accept_new_contact(df):
    df_accept = pd.DataFrame()

    # Loop
    for index, row in df.iterrows():
        fullname = row.FULLNAME
        status = row.INVITATION_STATUS
        invitation_id = row.INVITATION_ID
        shared_secret = row.SHARED_SECRET
        if status == "PENDING":
            print(fullname)
            tmp_df = linkedin.connect(li_at, JSESSIONID).invitation.accept(
                invitation_id, shared_secret
            )
            df_accept = pd.concat([df_accept, tmp_df])
    return df_accept


df_accept = accept_new_contact(df_invitation)
df_accept
```

### Send first message to contact


```python
def send_first_message(df):
    # Loop
    for index, row in df.iterrows():
        fullname = row.FULLNAME
        profile_id = row.PROFILE_ID
        print(fullname)
        linkedin.connect(li_at, JSESSIONID).message.send(FIRST_MESSAGE, profile_id)


send_first_message(df_accept)
```

## Output


### Display result



```python
df_accept
```

### Schedule notebook


```python
# Schedule your notebook every hour
naas.scheduler.add(cron=cron)

# -> Uncomment the line below to remove your scheduler
# naas.scheduler.delete()
```
