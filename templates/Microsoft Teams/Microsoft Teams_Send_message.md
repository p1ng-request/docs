<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Microsoft Teams - Send message
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Microsoft%20Teams/Microsoft%20Teams_Send_message.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #teams #microsoft

## Input

### Import library


```python
from naas_drivers import teams
```

### Connect to your Teams
[Click here to discover how to get your webhook](https://naas.gitbook.io/drivers/automation/teams)


```python
webhook = "https://forgr.webhook.office.com/webhookb2/83bcbd92-7095-48e9-bc59-60fb9f6dcf2e@da744f16-111c-41b2-899f-6332dfe22d16/IncomingWebhook/b3cf540a51d7465ca10bd85a61c10d92/c97dc097-a7ff-4123-865d-ac6482bcdac2"
```

## Model

### Set your message 


```python
message = "second test"
image_url = "http://i.imgur.com/c4jt321l.png" # Set to None if you don't need it
```

## Output

### Send it


```python
tm = teams.connect(webhook)
tm.send(message, image=image_url)
```
