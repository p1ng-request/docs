<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Find_all_users_on_workspace.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Find+all+users+on+workspace:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #workspace #users #find #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to find all users on a workspace using Clockify API.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/User/operation/getUsersOfWorkspace)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
```

## Model

### Get all users from workspace

This function will get all users from a workspace using Clockify API.


```python
def get_users_from_workspace(workspace_id, api_key):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/users"
    headers = {"X-Api-Key": api_key}
    response = requests.get(url, headers=headers)
    return response.json()

users = get_users_from_workspace(workspace_id, api_key)
```

## Output

### Display result


```python
print("Users found:", len(users), "\n")
for user in users:
    print("-", user["name"], f'(id: {user["id"]})')
if len(users) > 0:
    print()
    pprint(users[0])
```
