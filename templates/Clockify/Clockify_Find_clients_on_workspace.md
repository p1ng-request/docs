<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Find_clients_on_workspace.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Find+clients+on+workspace:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #workspace #client #api #python #find

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to find clients on a workspace using the Clockify API. It will return a dataframe with columns as follow:
- id: This column represents an identifier or unique identifier associated with a record or entity. It contains alphanumeric values that uniquely identify each row in the DataFrame.
- name: This column stores the name or title associated with a particular record or entity. It likely contains text values representing the name of a person, object, or entity.
- email: This column stores email addresses associated with the records in the DataFrame. It likely contains text values representing the email addresses of individuals or entities.
- workspaceId: This column represents an identifier or unique identifier associated with a workspace. It likely contains alphanumeric values that uniquely identify each workspace.
- archived: This column indicates whether a record or entity is archived or not. It likely contains boolean values (True or False), with True indicating that the record is archived and False indicating that it is not.
- address: This column stores addresses associated with the records in the DataFrame. It likely contains text values representing physical or postal addresses.
- note: This column stores additional notes or comments related to the records in the DataFrame. It may contain text values providing extra information or details about a particular record or entity.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Client/operation/getClients)
- [Clockify API Client Libraries](https://clockify.github.io/clockify_client_libraries/)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
```

## Model

### Find clients on workspace

This function will use the Clockify API to find clients on a workspace.


```python
def find_clients_on_workspace(workspace_id, api_key):
    # Set the request URL
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/clients"
    # Set the request headers
    headers = {"X-Api-Key": api_key}
    # Make the request
    response = requests.get(url, headers=headers)
    # Return the response
    return response.json()

# Find clients on workspace
clients = find_clients_on_workspace(workspace_id, api_key)
```

## Output

### Display result


```python
print("Clients found:", len(clients), "\n")
for client in clients:
    print("-", client["name"], f'(id: {client["id"]})')

df = pd.DataFrame(clients)
df
```

 
