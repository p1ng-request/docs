<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Send_email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Send+email:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #email #send #python #library #smtplib

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to send an email using naas_drivers. It is usefull for organizations that need to send emails from their Gmail account.

**References:**
- [Python smtplib](https://docs.python.org/3/library/smtplib.html)
- [Gmail SMTP server](https://support.google.com/a/answer/176600?hl=en)

## Input

### Import libraries


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
- `email_to`: This variable stores the email receiver address.
- `email_subject`: This variable stores the email subject.
- `email_msg`: This variable stores the email msg.


```python
# Inputs
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"

# Outputs
email_to = "xxxxx@xxxxx"
email_subject = "My First Email"
email_msg = "This is a test email"
```

## Model

### Connect to email box


```python
emails = email.connect(username, password, smtp_server=smtp_server)
```

## Output

### Send email


```python
emails.send(
    email_to=email_to,
    subject=email_subject,
    content=email_msg
)
```
