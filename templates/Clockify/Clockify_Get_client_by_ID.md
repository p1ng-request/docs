<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Get_client_by_ID.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Get+client+by+ID:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #client #create #api #rest #documentation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get a client using Clockify API from a specific workspace.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Client/operation/getClient)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace
- `client_id`: ID of the client to get


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
client_id = "626ff141e7dfbaxxxxx"
```

## Model

### Get client


```python
def get_client(workspace_id, api_key, client_id):
    url = f"https://api.clockify.me/api/workspaces/{workspace_id}/clients/{client_id}"
    headers = {
        "X-Api-Key": api_key,
        "Content-Type": "application/json"
    }
    response = requests.get(url, headers=headers)
    return response
```

## Output

### Display result


```python
response = get_client(workspace_id, api_key, client_id)
if response.status_code == 200:
    print(f"✅ Client '{client_id}' retrieved from workspace.")
else:
    print(f"❌ Error retrieving client")
response.json()
```

 
