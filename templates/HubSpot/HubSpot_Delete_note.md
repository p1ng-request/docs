<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Delete_note.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Delete+note:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #sales #crm #engagements #note #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This template deletes note with a note ID as input.

## Input

### Import libraries


```python
import requests
import json
import naas
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

#### Enter Your Access Token


```python
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Setup your note info


```python
note_id = 19996680052
```

## Model

### Function to delete note


```python
def delete_note(note_id):
    url = f"https://api.hubapi.com/crm/v3/objects/notes/{note_id}"
    headers = {
        "accept": "application/json",
        "content-type": "application/json",
    }
    params = {"limit": "100", "archived": "false", "hapikey": HS_API_KEY}
    # Requests data
    res = requests.delete(url, headers=headers, params=params)
    res.raise_for_status()
    if res.status_code == 204:
        print(f"❎ Note deleted in HubSpot: {note_id}")
```

## Output

### Delete note


```python
delete_note(note_id)
```
