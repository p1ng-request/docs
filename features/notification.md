---
Description: Send simple emails to anyone directly from your notebook.
---

# 🛎 Notification

### Introduction:
A notification is an alert sent to people.

Run the notification machine to effortlessly send emails from your notebooks.

Refer to the doc to install it.


## Text

Refer the below code to send an alert to anyone about the data changes and other notebook operations.

```python
import naas
email_to = "our@planet.com"
subject = "Hello world 👋🌏"
content = "Naas is here for you"

naas.notification.send(email_to=email_to, subject=subject, html=content)
```

## **Attachments**

Send the attachments from your notebook with minimal effort.

```python
import naas
email_to = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : [LINK]"'
files = ["path/to/my/super/data.csv"]

naas.notification.send(email_to=email_to, subject=subject, html=content, files=files)
```

## HTML &#x20;

Run the below script to send an image as hyperlink.

```python
import naas
email_to = "elon@musk.com"
subject = "The tesla action is going up"
image_path = "path/to/my/super/data.png"
content = f"<h1>Check in the link the chart image below</h1><br/> <img src="{image_path}"/>"

naas.notification.send(email_to=email_to, subject=subject, html=content)
```

## Custom sender&#x20;

Execute the below program to send emails to others from your mail ID

```python
import naas
email_to = "elon@musk.com"
email_from = "YOUR_NAAS_EMAIL_ACCOUNT"
# Admin can send with any mailbox
email_from = "tony@stark.com"
subject = "❤️ Check this email sent from Naas"
content = "I made this in 1 min. It's so easy to send emails with naas.ai"

naas.notification.send(email_to=email_to, subject=subject, html=content, email_from=email_from)
```

## List

Retrieve details of all the emails or notifications sent to you by the user.

```python
import naas
naas.notification.list()
```

## List all (Admin)

Retrieve the information of emails or notifications sent by users as an Admin

```python
import naas
naas.notification.list_all()
```
