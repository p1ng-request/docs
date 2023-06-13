<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Update_email_flag.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Update+email+flag:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #productivity #naas_drivers #operations #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook allows you to update an email flag in your Gmail inbox.

## Input

### Import librairy


```python
import naas
from naas_drivers import email
```

### Setup Variables
Create an application password following [this procedure](https://support.google.com/mail/answer/185833?hl=en)
- `username`: This variable stores the username or email address associated with the email account
- `password`: This variable stores the password or authentication token required to access the email account
- `smtp_server`: This variable represents the SMTP server address used for sending emails.
- `box`: This variable stores the name or identifier of the mailbox or folder within the email account that will be accessed.
- `uid`: Unique email ID to be updated. You can it by reading your mailbox.
- `flag`: possible value for flag: 'SEEN', 'ANSWERED', 'FLAGGED', 'DELETED', 'DRAFT', 'RECENT'


```python
# Inputs
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"

# Outputs
uid = "7907"
flag = "SEEN"
```

## Model

### Connect to email box


```python
emails = email.connect(username, password, smtp_server=smtp_server)
```

## Output

### Update email status


```python
emails.set_flag(uid, flag)
```
