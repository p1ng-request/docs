<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Gmail/Gmail_Create_GitHub_issue_on_specific_email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Gmail+-+Create+GitHub+issue+on+specific+email:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gmail #github #email #issue #create #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create a GitHub issue from a specific email using Gmail and Python. It is usefull for organizations that need to track emails and create issues from them.

**References:**
- [Gmail API](https://developers.google.com/gmail/api)
- [GitHub API](https://developer.github.com/v3/)

## Input

### Import librairies


```python
import naas
from naas_drivers import email
from re import search
import pandas as pd
import requests
```

### Setup Variables
Create an application password following [this procedure](https://support.google.com/mail/answer/185833?hl=en)
- `username`: This variable stores the username or email address associated with the email account
- `password`: This variable stores the password or authentication token required to access the email account
- `smtp_server`: This variable represents the SMTP server address used for sending emails.
- `box`: This variable stores the name or identifier of the mailbox or folder within the email account that will be accessed.
- `keywords`: This variable stores the keywords to be searched in email text.
- `cron`: CRON to be set to schedule your notebook. More info [here](https://crontab.guru/)
- `github_token`: GitHub token
- `repository_url`: GitHub HTML repository URL
- `assignees`: GitHub assignees
- `labels`: GitHub labels


```python
# Inputs
username = "xxxxx@xxxx"
password = naas.secret.get("GMAIL_APP_PASSWORD") or "xxxxxxxx"
smtp_server = "imap.gmail.com"
box = "INBOX"
keywords = "xxxx"

# Outputs
cron = "0 8,20 * * *" #everyday at 8AM and 8PM
github_token = naas.secret.get('GITHUB_TOKEN')
repository_url = "https://github.com/xxxxxxx"
assignees = []
labels = []
```

## Model

### Get email list


```python
emails = email.connect(username, password, smtp_server=smtp_server)
df_emails = emails.get()
print(f"✅ Emails fetched:", len(df_emails))
df_emails.head(1)
```

### Find emails matching criteria on subject and text


```python
def find_match(df, keywords):
    # Init
    df_match = pd.DataFrame()
    
    # Loop
    for index, row in df.iterrows():
        tmp_df = pd.DataFrame()
        uid = row["uid"]
        subject = row["subject"]
        text = row["text"]
        
        # Check keywords on subject and text
        if search(keywords, subject):
            tmp_df = df[index:index+1]
        elif search(keywords, text):
            tmp_df = df[index:index+1]
        if len(tmp_df) > 0:
            df_match = pd.concat([df_match, tmp_df])
    return df_match.reset_index(drop=True)
    
df_match = find_match(df_emails, keywords)
print("✅ Rows fetched:", len(df_match))
df_match.head(1)
```

## Output

### Create GitHub issue and delete email


```python
def create_new_github_issue(
    token,
    repository_url,
    subject,
    text,
    assignees,
    labels,
):
    # Init
    title = subject.replace("Fwd:", "")
    body = text
    
    # Requests
    owner = repository_url.split("github.com/")[-1].split("/")[0]
    repo_name = repository_url.split(f"/{owner}/")[-1].split("/")[0]
    url = f"https://api.github.com/repos/{owner}/{repo_name}/issues"
    data = {
        "title": title,
        "body": body,
        "assignees": assignees,
        "labels": labels,
    }
    headers = {'Authorization': f'token {token}'}
    response = requests.post(url, headers=headers, json=data)
    github_issue = response.json()
    print(f"✅ Github issue created:", f"https://github.com/{owner}/{repo_name}/issues/{github_issue.get('number')}")
    return github_issue

if len(df_match) > 0:
    for index, row in df_match.iterrows():
        uid = row["uid"]
        subject = row["subject"]
        text = row["text"]
        create_new_github_issue(
            github_token,
            repository_url,
            subject,
            text,
            assignees,
            labels
        )
        emails.set_flag(uid, name="DELETED")
        print("✅ Email deleted from mailbox")
```

### Add scheduler


```python
naas.scheduler.add(cron=cron)
```

 
