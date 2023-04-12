    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_Task.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Update+Task:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #sales #crm #engagements #task #snippet

**Author:** [Alok Chilka](https://www.linkedin.com/in/calok64/)

**Description:** This template will update a task in HubSpot. 

## Input

### Import libraries


```python
from datetime import datetime, timedelta
from naas_drivers import hubspot
import requests, math
import json
import naas
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

#### Enter Your Access Token


```python
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Define your task info


```python
task_id = 19996848972
owner_id = 111111086
subject = "Task updated"
body = "This is third update"
time_delay = 1
```

## Model

### Function to update task


```python
def patch(uid, data):
    # set headers
    headers = {
        "Content-Type": "application/json",
        "authorization": f"Bearer {HS_ACCESS_TOKEN}",
    }
    base_url = "https://api.hubapi.com/engagements/v1/engagements/"
    res = requests.patch(
        url=f"{base_url}/{uid}",
        headers=headers,
        params=params,
        json=data,
        allow_redirects=False,
    )
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        return e
    # Message success
    print(f"✔️ successfully updated.")
    return res.json()
```


```python
def update_task(task_id, owner_id, subject, body, time_delay):

    # set headers
    url = "https://api.hubapi.com/engagements/v1/engagements/"
    params = {"hapikey": HS_API_TOKEN}
    headers = {"Content-Type": "application/json"}

    # Calc timestamp to set delay
    tstampobj = datetime.now() + timedelta(days=time_delay)
    tstamp = tstampobj.timestamp() * 1000

    # check if tasks already exist

    get_task = requests.get(
        url=f"{get_url}/{task_id}",
        headers=headers,
        params=params,
        allow_redirects=False,
    )

    if get_task.status_code == 200:
        print("Task found..Updating")

        # Update Task
        data = {
            "engagement": {
                "ownerId": owner_id,
                "timestamp": tstamp,
            },
            "metadata": {
                # "type": "TASK",
                "body": body,
                # "status": "NOT_STARTED", # NOT_STARTED | COMPLETED | IN_PROGRESS | WAITING | DEFERRED
                # "forObjectType": "CONTACT",
                # "subject": subject,
            },
        }

        patch(task_id, data)

    else:
        print("Task not found. Unable to update")
```

## Output

### Update task


```python
update_task(task_id, owner_id, subject, body, time_delay)
```
