<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Slack - Send message
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Slack/Slack_Send_message.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #slack #message #send

## Input

### Import needed library


```python
from naas_drivers import slack
```

### Put your slack token
[Click here to discover how to get your token](https://naas.gitbook.io/drivers/automation/slack)


```python
token = "xoxb-232887839156-1673274923699-vTF6NOKOMosoPFI7qfnkCdRF"
```

## Model

### Set your message 


```python
channel = "-team-tech"
message = "second test"
image_url = "http://i.imgur.com/c4jt321l.png" # Set to None if you don't need it
```

## Output

### Send it


```python
sk = lack.connect(token)
sk.send(channel, "second test", image=image_url)
```
