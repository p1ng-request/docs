<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Delete_Task.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Delete+Task:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #sales #crm #engagements #task #snippet

**Author:** [Alok Chilka](https://www.linkedin.com/in/calok64/)

**Description:** This template will delete a task in HubSpot. 

## Input

### Import libraries


```python
from datetime import datetime, timedelta
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

#### Enter your task ID


```python
task_id = 19996680052
```

## Model

### Function to get recent tasks


```python
def delete_task(uid):
    # set headers
    headers = {
        "Content-Type": "application/json",
        "authorization": f"Bearer {HS_ACCESS_TOKEN}",
    }

    # check if tasks already exist
    get_url = "https://api.hubapi.com/engagements/v1/engagements/"
    get_res = requests.get(
        url=f"{get_url}/{uid}",
        headers=headers,
        allow_redirects=False,
    )
    if get_res.status_code == 200:
        print("Task found..Deleting")
        # delete task
        del_url = "http://api.hubapi.com/engagements/v1/engagements/"

        # Post requests
        res = requests.delete(
            url=f"{url}/{uid}",
            headers=headers,
            params=params,
            allow_redirects=False,
        )
    else:
        print("Task not found. Unable to delete")
```

## Output

### Delete task


```python
delete_task(task_id)
```


```python

```
