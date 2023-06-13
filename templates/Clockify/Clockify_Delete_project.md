<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Delete_project.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Delete+project:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #project #create #api #rest #documentation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to delete an existing project using Clockify API from a specific workspace. You can only delete archived project. Active project can not be deleted.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Project/operation/delete_6)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace
- `project_id`: ID of the project to be deleted


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
project_id = "6465128cb3aa2432050af887"
```

## Model

### Delete project

This function will delete an existing project using Clockify API.


```python
def delete_project(api_key, workspace_id, project_id):
    url = f"https://api.clockify.me/api/workspaces/{workspace_id}/projects/{project_id}"
    headers = {
        "X-Api-Key": api_key,
        "Content-Type": "application/json"
    }
    response = requests.delete(url, headers=headers)
    return response
```

## Output

### Display result


```python
response = delete_project(api_key, workspace_id, project_id)
if response.status_code == 200:
    print(f"✅ Client '{project_id}' deleted from workspace")
else:
    print(f"❌ Error while deleted project '{project_id}'")
response.json()
```

 
