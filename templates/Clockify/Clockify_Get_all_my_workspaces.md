<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Get_all_my_workspaces.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Get+all+my+workspaces:+Error+short+description">Bug report</a>

**Tags:** #clockify #api #workspace #get #python #rest

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to get all workspaces of a user using the Clockify API.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Workspace/operation/getWorkspacesOfUser)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
```

## Model

### Get all workspaces

This function will get all workspaces of a user using the Clockify API.


```python
def get_workspaces(api_key):
    url = "https://api.clockify.me/api/workspaces"
    headers = {"X-Api-Key": api_key}
    response = requests.get(url, headers=headers)
    return response.json()

workspaces = get_workspaces(api_key)
```

## Output

### Display result


```python
print("Workspaces found:", len(workspaces), "\n")
pprint(workspaces)
```

 
