<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Add_a_new_project.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Add+a+new+project:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #project #create #api #rest #documentation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to add a new project using Clockify API to a specific workspace.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Project/operation/create_6)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace
- `payload`: Data of the project to be created


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
payload = {
    "name": "My New Project",
    "note": "Notes",
    "public": True,
    "billable": True,
    "clientId": None,
    "color": "#000000",
}
```

## Model

### Create new project

This function will create a new project using Clockify API.


```python
def create_project(api_key, workspace_id, payload):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/projects"
    headers = {
        "X-Api-Key": api_key,
        "Content-Type": "application/json"
    }
    response = requests.post(url, headers=headers, json=payload)
    return response
```

## Output

### Display result


```python
response = create_project(api_key, workspace_id, payload)
if response.status_code == 201:
    print(f"✅ Project '{response.json().get('id')}' created to workspace")
else:
    print(f"❌ Error added new project")
response.json()
```

 
