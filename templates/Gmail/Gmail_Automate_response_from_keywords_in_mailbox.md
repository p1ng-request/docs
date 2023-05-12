<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Automate_response_from_keywords_in_mailbox.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Automate+response+from+keywords+in+mailbox:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #productivity #naas_drivers #operations #snippet

**Author:** [Sanjay Sabu](https://www.linkedin.com/in/sanjay-sabu-4205/)

**Description:** This notebook automates the process of responding to emails in Gmail based on keywords found in the mailbox.

## Input

### Import librairies


```python
import naas
from naas_drivers import email
from re import search
```

### Setup Variables
Create an application password following [this procedure](https://support.google.com/mail/answer/185833?hl=en)
- `username`: This variable stores the username or email address associated with the email account
- `password`: This variable stores the password or authentication token required to access the email account
- `smtp_server`: This variable represents the SMTP server address used for sending emails.
- `box`: This variable stores the name or identifier of the mailbox or folder within the email account that will be accessed.
- `keywords`: This variable stores the keywords to be searched in email text.
- `cron`: CRON to be set to schedule your notebook. More info [here](https://crontab.guru/)
- `email_to`: This variable stores the emails to received the automatic response.
- `subject`: This variable stores the subject of the email response.
- `content`: This variable stores the content of the email response.
- `files`: This variable stores the files to be sent as attachments.


```python
# Inputs
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"
keywords = "sales report"

# Outputs
cron = "0 20 * * *" #everyday at 8PM
email_to = "xxxx@xxxxx"
subject = "Sales Report"
content = "Hi \n,Here I am attaching the sales report as per your request\n.With Regards\n,NAAS Team"
files = []
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

### Automated reponse


```python
for df in dataframe["text"]:
    text = df.lower()
    if search(keywords, text):
        naas.notifications.send(
            email_to=email_to,
            subject=subject,
            html=content,
            files=files
        )
```
