<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Update_project.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Update+project:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #project #create #api #rest #documentation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to update a project using Clockify API from a specific workspace.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Project/operation/update_4)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace
- `project_id`: ID of the project to get
- `payload`: data to be updated


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
project_id = "63c7ac83978e3a0c21495757"
payload = {
    "name": "string",
    "note": "string",
    "isPublic": True,
    "archived": True,
    "billable": True,
    "clientId": "string",
    "color": "string",
    "costRate": {
        "amount": 0,
        "since": "string"
        },
    "hourlyRate": {
        "amount": 0,
        "since": "string"
        },
}
```

## Model

### Update project


```python
def update_project(api_key, workspace_id, project_id, payload):
    url = f"https://api.clockify.me/api/workspaces/{workspace_id}/projects/{project_id}"
    headers = {
        "X-Api-Key": api_key,
        "Content-Type": "application/json"
    }
    response = requests.put(url, headers=headers, json=payload)
    return response
```

## Output

### Display result


```python
response = update_project(api_key, workspace_id, project_id, payload)
if response.status_code == 200:
    print(f"✅ Project '{project_id}' update from workspace.")
else:
    print(f"❌ Error retrieving project")
response.json()
```

 
