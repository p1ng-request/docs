<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Get_seen_emails.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Get+seen+emails:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #productivity #naas_drivers #operations #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook allows you to read your Gmail inbox and get the seen emails. It returns a dataframe as follow:
- uid: This column represents the unique identifier associated with each row or email in the dataframe.
- subject: The subject column contains the subject line or title of the email.
- from: The "from" column contains information about the sender of the email. It includes the email address and name of the sender.
- to: The "to" column contains information about the primary recipients of the email. It includes the email addresses and names of the recipients.
- cc: The "cc" column represents the carbon copy recipients of the email. It contains a list of email addresses and names of the cc'd recipients.
- bcc: The "bcc" column contains the blind carbon copy recipients of the email. Similar to the "cc" column, it includes a list of email addresses and names.
- reply_to: This column contains the email addresses and names that should be used when replying to the email.
- date: The "date" column indicates the date and time when the email was sent.
- text: The "text" column contains the plain text content of the email.
- html: The "html" column includes the HTML-formatted content of the email.
- flags: The "flags" column represents any flags or indicators associated with the email, such as important, starred, etc.
- headers: This column contains additional headers of the email, such as the "delivered-to," "received," and "X-Google-Smtp-Source" headers.
- size_rfc822: The "size_rfc822" column indicates the size of the email in RFC822 format.
- size: The "size" column represents the size of the email in bytes.
- obj: The "obj" column contains the object representation of the email.
- attachments: This column includes any attachments associated with the email, such as files, images, etc.

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
- `criteria`: by default "ALL" is returned but you can also filter on "unseen" or "seen" emails


```python
# Inputs
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"
criteria = "seen"
```

## Model

### Connect to email box


```python
emails = email.connect(username, password, smtp_server=smtp_server)
```

## Output

### Get email list


```python
df = emails.get(box=box, criteria=criteria).sort_values(by="date", ascending=False)
print(f"✅ Emails '{criteria}' fetched:", len(df))
df
```
