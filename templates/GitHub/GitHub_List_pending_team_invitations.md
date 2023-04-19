<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_pending_team_invitations.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+pending+team+invitations:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #teams #invitations #rest #api #list #snippet

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to list pending team invitations using the GitHub REST API and will create a DataFrame as output. It can be used by organizations with multiple teams on GitHub to keep track of pending team invitations, ensuring that all team members are added to the appropriate teams and can collaborate effectively. It helps in managing team membership and permissions for efficient collaboration within the organization.

**References:**
- [GitHub REST API - List pending team invitations](https://docs.github.com/fr/rest/teams/members?apiVersion=2022-11-28#list-pending-team-invitations)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
from pprint import pprint
```

### Setup Variables
- `token`: Create your personal access token [here](https://github.com/settings/tokens)
- `team_url`: The URL of the team to list pending invitations for.


```python
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_TOKEN"
team_url = "https://github.com/orgs/jupyter-naas/teams/opensource-contributors"
```

## Model

### List pending team invitations
This function will list pending team invitations using the GitHub REST API.


```python
def list_pending_team_invitations(team_url):
    org = team_url.split("/orgs/")[-1].split("/")[0]
    team_slug = team_url.split("/teams/")[-1]
    url = f"https://api.github.com/orgs/{org}/teams/{team_slug}/invitations"
    response = requests.get(url)
    headers = {"Authorization": f"token {token}"}
    res = requests.get(url, headers=headers)
    if res.status_code == 200:
        return res.json()

pending_invitations = list_pending_team_invitations(team_url)
```

## Output

### Display result


```python
# Flatten the nested dict
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

data = []
for d in pending_invitations:
    data.append(flatten_dict(d))
    
df_pending_invitations = pd.DataFrame(data)
print("Pending invitations found:", len(df_pending_invitations))
df_pending_invitations
```

 
