---
description: Send simple email from your notebooks
---

# Notification

## Simple

Send and email notification to anyone,  notify data have change, notebook have run etc.. 

```python
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : [LINK]"
naas.notifications.send(email=email, subject=subject, content=content)
```

