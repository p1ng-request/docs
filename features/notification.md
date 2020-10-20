---
description: Send simple email from your notebooks
---

# 🛎️ Notifications

## Text

Send an email notification to anyone, notify about data changes, alert on notebooks operations, etc... 

```python
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : [LINK]"

naas.notifications.send(email_to=email, subject=subject, html=content)
```

## File

```python
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : [LINK]"'
files = ["path/to/my/super/data.csv"]

naas.notifications.send(email_to=email, subject=subject, html=content, files=files)
```

## HTML

```python
email = "elon@musk.com"
subject = "The tesla action is going up"
image_path = "path/to/my/super/data.png"
html = f"<h1>Check in the link the chart image below</h1><br/> <img src="{image_path}"/>"

naas.notifications.send(email_to=email, subject=subject, html=content)
```

## Custom sender

```python
email_to = "elon@musk.com"
email_from = "bob@cahstory.com"
subject = "The tesla action is going up"
image_path = "path/to/my/super/data.png"
html = f"<h1>Check in the link the chart image below</h1><br/> <img src="{image_path}"/>"

naas.notifications.send(email_to=email, subject=subject, html=content, email_from=email_from)
```



