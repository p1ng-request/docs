<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Scheduler_demo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #scheduler

Read the doc: https://naas.gitbook.io/naas/features/scheduler

Transform all your work routines in notebooks and run them even when you sleep.

## Input

### Import library


```python
import naas
```

Here we are going to use the Notifications feature to test Scheduler.

## Model

### Content of the mail


```python
email_to = "jeremy.ravenel@cashstory.com"
subject = "Naas Scheduler Test"
content ='''<p>If i put html in there..&nbsp;</p>
<p><img src="https://specials-images.forbesimg.com/imageserve/5f1f37a40a5db2c8275972c0/960x0.jpg?fit=scale" alt="" width="959" height="663" /></p>'''
```

## Output

### Send the email


```python
naas.notifications.send(email_to, subject, content)
```

### Setting up the scheduler


```python
naas.scheduler.add(recurrence="0 1 * * *")
```
