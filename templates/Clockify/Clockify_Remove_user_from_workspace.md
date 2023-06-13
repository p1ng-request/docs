<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Remove_user_from_workspace.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Remove+user+from+workspace:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #workspace #remove #user #api #rest

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to remove a user from a workspace using the Clockify API.

**References:**
- [Clockify API Documentation](https://clockify.me/developers-api)
- [Clockify Workspace Documentation](https://docs.clockify.me/#tag/Workspace/operation/removeMember)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace from which the user will be removed.
- `user_id`: ID of the user to be removed.


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
user_id = "<YOUR_USER_ID>"
```

## Model

### Remove user from workspace

This function removes a user from a workspace using the Clockify API.


```python
def remove_user_from_workspace(api_key, workspace_id, user_id):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/users/{user_id}"
    headers = {"X-Api-Key": api_key}
    response = requests.delete(url, headers=headers)
    return response
```

## Output

### Display result


```python
response = remove_user_from_workspace(api_key, workspace_id, user_id)
if response.status_code == 200:
    print(f"✅ User '{user_id}' deleted from workspace")
else:
    print(f"❌ Error while deleted user '{user_id}'")
```

 
