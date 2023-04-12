    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Create_note.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Create+note:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #sales #crm #engagements #notes #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This template will create a note in HubSpot with the possibility of :
- Add timestamp to follow history
- Add associated contacts
- Add associated companies
- Add associated deals
- Add creator
- Add multiples owners

## Input

### Import libraries


```python
from datetime import datetime
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

#### Define your note


```python
# Note content => HTML format can be used to create custom notes (Required)
body = "My new note"  # EXAMPLE: "My new notes"

# Note timestamp in format "%Y-%m-%d %H:%M:%S" (Not mandatory)
timestamp = "2022-05-31 08:13:00"  # EXAMPLE: "2022-05-31 08:13:00"

# Associated contacts ID (Required)
asso_contactids = []  # EXAMPLE: [00001] or [00001, 00002, 000003]

# Associated companies ID (Not mandatory)
asso_companyids = []  # EXAMPLE: [00001] or [00001, 00002, 000003]

# Associated deals ID (Not mandatory)
asso_dealids = []  # EXAMPLE: [00001] or [00001, 00002, 000003]

# Associated owners ID (Not mandatory)
asso_ownerids = []  # EXAMPLE: [00001] or [00001, 00002, 000003]

# Creator ID (Not mandatory)
owner_id = None
```

## Model

### Function to create note


```python
def create_note(
    body,
    timestamp=None,
    owner_id=None,
    asso_contactids=[],
    asso_companyids=[],
    asso_dealids=[],
    asso_ownerids=[],
    engagement="NOTE",
):
    """
    Engagement type = NOTE
    """

    # Calc timestamp
    if timestamp is not None:
        timestamp = (
            str(int(datetime.strptime(timestamp[:19], "%Y-%m-%d %H:%M:%S").timestamp()))
            + "000"
        )
    else:
        timestamp = str(int(datetime.now().timestamp())) + "000"

    # Create payload
    payload = json.dumps(
        {
            "engagement": {
                "active": "true",
                "ownerId": owner_id,
                "type": engagement,
                "timestamp": timestamp,
            },
            "associations": {
                "contactIds": asso_contactids,
                "companyIds": asso_companyids,
                "dealIds": asso_dealids,
                "ownerIds": asso_ownerids,
            },
            "metadata": {
                "body": body,
            },
        }
    )
    url = "https://api.hubapi.com/engagements/v1/engagements"
    headers = {
        "Content-Type": "application/json",
        "authorization": f"Bearer {HS_ACCESS_TOKEN}",
    }
    # Post requests
    res = requests.post(url, data=payload, headers=headers)
    res.raise_for_status()
    res_json = res.json()
    # Note ID
    note_id = res_json.get("engagement").get("id")
    # Message success
    print(f"✅ New note created '{note_id} 'in HubSpot: {body}")
    return note_id
```

## Output

### Create note


```python
note_id = create_note(
    body=body,
    timestamp=timestamp,
    asso_contactids=asso_contactids,
    asso_companyids=asso_companyids,
    asso_dealids=asso_dealids,
    asso_ownerids=asso_ownerids,
    owner_id=owner_id,
)
```
