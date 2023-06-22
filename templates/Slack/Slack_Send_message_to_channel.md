<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Slack/Slack_Send_message_to_channel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Slack+-+Send+message:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #slack #message #send #operations #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows you to quickly and easily send text messages through Slack.

**References:**
- [Sending messages](https://api.slack.com/messaging/sending)

## Input

### Import needed library


```python
from naas_drivers import slack
import naas
```

### Setup Variables
- Create [Slack App](https://api.slack.com/apps)
- Add OAuth & Permissions(chat:write, chat:write.public to send message in a public channel)
- Install your App
- Get your Bot Token

Once it's done, update the variables below and run the notebook.

- `slack_token`: This is where you place the Bot token
- `slack_channel`: the channel where you wish to send the message
- `text_message`: the message you wish to send


```python
slack_token = naas.secret.get("SLACK_TOKEN") or "SLACK_TOKEN"
slack_channel = "channel-name" 
text_message = "Hello World!"
```

## Model

### Connect to Slack


```python
SLACK = slack.connect(slack_token)
```

## Output

### Send your message 


```python
SLACK.send(slack_channel, text_message)
```
