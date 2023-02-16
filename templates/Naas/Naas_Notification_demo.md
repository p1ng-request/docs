<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Notification_demo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Notification+demo:+Error+short+description">Bug report</a>

**Tags:** #naas #notification #snippet #operations

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook demonstrates how to use Naas to send notifications.

## Input

### Import library


```python
import naas
```

## Model

### Notification informations


```python
email_to = "jeremy@acme.com"
subject = "🛎️ Naas Notification Test 🚨"
content = """<p>If i can see an image below this text...&nbsp;</p>
<p><img src="https://specials-images.forbesimg.com/imageserve/5f1f37a40a5db2c8275972c0/960x0.jpg?fit=scale" alt="" width="959" height="663" /></p><br>
...it means everything goes well."""
```

## Output

### Send the notification


```python
naas.notification.send(email_to, subject, content)
```
