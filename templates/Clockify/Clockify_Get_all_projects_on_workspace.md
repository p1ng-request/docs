    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Get_all_projects_on_workspace.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Get+all+projects+on+workspace:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #api #projects #workspace #get #python

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to get all projects on a workspace using the Clockify API and return a dict.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Project/operation/getProjects)

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

### Get all projects on workspace

This function will get all projects on a workspace using the Clockify API.


```python
def get_projects(api_key, workspace_id):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/projects"
    headers = {"X-Api-Key": api_key}
    response = requests.get(url, headers=headers)
    return response.json()

projects = get_projects(api_key, workspace_id)
```

## Output

### Display result


```python
print("Projects found:", len(projects), "\n")
for project in projects:
    print("-", project["name"])
if len(projects) > 0:
    print()
    pprint(projects[0])
```

 
