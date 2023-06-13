<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Add_or_update_team_membership_for_a_user.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Add+or+update+team+membership+for+a+user:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #teams #members #api #rest #python

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook add or update team membership for a user.

**References:**
- [GitHub - Add or update team membership for a user](https://docs.github.com/fr/rest/teams/members?apiVersion=2022-11-28#add-or-update-team-membership-for-a-user)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `token`: [GitHub personal access token](https://github.com/settings/tokens)
- `org_id`: ID of the organization
- `team_id`: ID of the team
- `username`: GitHub username
- `role`: The role that this user should have in the team. Can be one of: `maintainer`, `member`.


```python
token = naas.secret.get("GITHUB_TOKEN") or "GITHUB_TOKEN"
org_id = "jupyter-naas"
team_id = "<team_id>"
username = "<username>"
role = "member"
```

## Model

### Add or update team membership for a user


```python
def update_team_membership(token, org, team, username, role):
    # Init
    res_json = None
    
    # Request
    url = f"https://api.github.com/orgs/{org}/teams/{team}/memberships/{username}"
    payload = {"role": role}
    headers = {
        "Authorization": f"token {token}",
        "Accept": "application/vnd.github.hellcat-preview+json",
    }
    res = requests.put(url, headers=headers, json=payload)
    
    # Result
    if res.status_code == 200:
        print(f"✅ User '{username}' updated in '{org}/{team}'")
        res_json = res.json()
    else:
        print(f"❌ User not updated in '{org}/{team}'")
    return res_json
```

## Output

### Display result


```python
membership = update_team_membership(token, org_id, team_id, username, role)
if membership:
    print(membership)
```
