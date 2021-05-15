---
description: Send simple email from your notebooks
---

# 🛎️ Notification

{% hint style="info" %}
In local you need to run the notification machine to make it work. refer to the doc to install it.
{% endhint %}

## Text

Send an email notification to anyone, notify about data changes, alert on notebooks operations, etc... 

```python
import naas
email_to = "our@planet.com"
subject = "Hello world 👋🌏"
content = "Naas is here for you"

naas.notification.send(email_to=email_to, subject=subject, html=content)
```

## **Attachments**

```python
import naas
email_to = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : [LINK]"'
files = ["path/to/my/super/data.csv"]

naas.notification.send(email_to=email_to, subject=subject, html=content, files=files)
```

## HTML  

```python
import naas
email_to = "elon@musk.com"
subject = "The tesla action is going up"
image_path = "path/to/my/super/data.png"
content = f"<h1>Check in the link the chart image below</h1><br/> <img src="{image_path}"/>"

naas.notification.send(email_to=email_to, subject=subject, html=content)
```

## Custom sender 

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

Allows retrieving the details of emails/notifications sent by the user.

```python
import naas
naas.notification.list()
```

## List all \(Admin\)

Allows retrieving the details of emails/notifications sent by all users as admin.

```python
import naas
naas.notification.list_all()
```

