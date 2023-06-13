<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Get_emails_stats_by_sender.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Get+emails+stats+by+sender:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #productivity #naas_drivers #operations #automation #analytics #plotly

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to get stats from their emailbox by sender.

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


```python
username = "xxxxx@xxxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD")
smtp_server = "imap.gmail.com"
box = "INBOX"
```

## Model

### Connect to email box


```python
emails = email.connect(username, password, username, smtp_server)
```

### Get email list


```python
df_emails = emails.get()
print(f"✅ Emails fetched:", len(df_emails))
df_emails.head(1)
```

### Creating dataframe and inserting values


```python
sender_name = []
sender_email = []
for df in df_emails["from"]:
    sender_name.append(df["name"])
    sender_email.append(df["email"])
    
result = pd.DataFrame(columns=["SENDER_NAME", "SENDER_EMAIL", "COUNT", "PERCENTAGE"])
name_unique = np.unique(sender_name)
email_unique = np.unique(sender_email)
total_email = len(df_emails)
c = 0
for i in np.unique(sender_name):
    new_row = {
        "SENDER_NAME": i,
        "SENDER_EMAIL": sender_email[c],
        "COUNT": sender_name.count(i),
        "PERCENTAGE": round(((sender_name.count(i)) / total_email) * 100),
    }
    result = result.append(new_row, ignore_index=True)
    c += 1
result
```

## Output

### Email graph plot


```python
fig = px.bar(x=result["COUNT"], y=result["SENDER_NAME"], orientation="h")
fig.show()
```
