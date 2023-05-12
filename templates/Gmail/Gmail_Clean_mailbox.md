<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Clean_mailbox.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Clean+mailbox:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #productivity #naas_drivers #operations #automation #scheduler

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook helps you quickly and easily organize your Gmail inbox by removing unwanted emails.

## Input

### Import libraries


```python
import naas
from naas_drivers import email
import pandas as pd
import numpy as np
import plotly.express as px
```

### Setup Variables
Create an application password following [this procedure](https://support.google.com/mail/answer/185833?hl=en)
- `username`: This variable stores the username or email address associated with the email account
- `password`: This variable stores the password or authentication token required to access the email account
- `smtp_server`: This variable represents the SMTP server address used for sending emails.
- `box`: This variable stores the name or identifier of the mailbox or folder within the email account that will be accessed.
- `remove_emails_from`: This variable stores the list of emails to be deleted in your email box
- `cron`: CRON to be set to schedule your notebook. More info [here](https://crontab.guru/)


```python
# Inputs
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"
remove_emails_from = ["notifications@naas.ai"]

# Outputs
cron = "0 20 * * *" #everyday at 8PM
```

## Model

### Connect to email box


```python
emails = email.connect(username, password, smtp_server=smtp_server)
```

### Get email list


```python
df_emails = emails.get()
print(f"✅ Emails fetched:", len(df_emails))
df_emails.head(1)
```

## Output

### Deleting using email id


```python
for index, df in enumerate(df_emails["from"]):
    sender_email = df["email"]
    uid = df_emails.loc[index, "uid"]
    subject = df_emails.loc[index, "subject"]
    if sender_email in remove_emails_from:
        emails.set_flag(uid, "DELETED")
        print(f"✅ Email '{subject}' from '{sender_email}' removed from mailbox.")
```

### Schedule notebok


```python
naas.scheduler.add(cron=cron)
```
