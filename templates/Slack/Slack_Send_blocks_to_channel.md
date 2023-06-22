<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Slack/Slack_Send_blocks_to_channel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Slack+-+Send+blocks+to+channel:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #slack #message #send #operations #snippet #block

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook allows you to quickly and easily send blocks through Slack. Blocks are visual components that can be stacked and arranged to create app layouts. Block Kit can make your app's communication clearer while also giving you consistent opportunity to interact with and assist users.

**References:**
- [Reference: Layout blocks](https://api.slack.com/reference/block-kit/blocks)
- [Building with Block Kit](https://api.slack.com/block-kit/building)
- [Block Kit Builder](https://app.slack.com/block-kit-builder)

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
- `blocks`: Custom blocks you wish to send


```python
slack_token = naas.secret.get("SLACK_TOKEN") or "SLACK_TOKEN"
slack_channel = "channel-name" 
blocks = [
    {
        "type": "section",
        "text": {
            "type": "mrkdwn",
            "text": "Hello, Assistant to the Regional Manager Dwight! *Michael Scott* wants to know where you'd like to take the Paper Company investors to dinner tonight.\n\n *Please select a restaurant:*"
        }
    },
    {
        "type": "divider"
    },
    {
        "type": "section",
        "text": {
            "type": "mrkdwn",
            "text": "*Farmhouse Thai Cuisine*\n:star::star::star::star: 1528 reviews\n They do have some vegan options, like the roti and curry, plus they have a ton of salad stuff and noodles can be ordered without meat!! They have something for everyone here"
        },
        "accessory": {
            "type": "image",
            "image_url": "https://s3-media3.fl.yelpcdn.com/bphoto/c7ed05m9lC2EmA3Aruue7A/o.jpg",
            "alt_text": "alt text for image"
        }
    },
    {
        "type": "section",
        "text": {
            "type": "mrkdwn",
            "text": "*Kin Khao*\n:star::star::star::star: 1638 reviews\n The sticky rice also goes wonderfully with the caramelized pork belly, which is absolutely melt-in-your-mouth and so soft."
        },
        "accessory": {
            "type": "image",
            "image_url": "https://s3-media2.fl.yelpcdn.com/bphoto/korel-1YjNtFtJlMTaC26A/o.jpg",
            "alt_text": "alt text for image"
        }
    },
    {
        "type": "section",
        "text": {
            "type": "mrkdwn",
            "text": "*Ler Ros*\n:star::star::star::star: 2082 reviews\n I would really recommend the  Yum Koh Moo Yang - Spicy lime dressing and roasted quick marinated pork shoulder, basil leaves, chili & rice powder."
        },
        "accessory": {
            "type": "image",
            "image_url": "https://s3-media2.fl.yelpcdn.com/bphoto/DawwNigKJ2ckPeDeDM7jAg/o.jpg",
            "alt_text": "alt text for image"
        }
    },
    {
        "type": "divider"
    },
    {
        "type": "actions",
        "elements": [
            {
                "type": "button",
                "text": {
                    "type": "plain_text",
                    "text": "Farmhouse",
                    "emoji": True
                },
                "value": "click_me_123"
            },
            {
                "type": "button",
                "text": {
                    "type": "plain_text",
                    "text": "Kin Khao",
                    "emoji": True
                },
                "value": "click_me_123",
                "url": "https://google.com"
            },
            {
                "type": "button",
                "text": {
                    "type": "plain_text",
                    "text": "Ler Ros",
                    "emoji": True
                },
                "value": "click_me_123",
                "url": "https://google.com"
            }
        ]
    }
]
```

## Model

### Connect to Slack


```python
SLACK = slack.connect(slack_token)
```

## Output

### Send your message 


```python
SLACK.send(slack_channel, text="", blocks=blocks)
```
