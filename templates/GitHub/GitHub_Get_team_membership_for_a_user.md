<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_team_membership_for_a_user.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+team+membership+for+a+user:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #teams #members #rest #api #python #snippet

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook get team membership for a user. It will return a dictionary with the state, role and url of the membership.

**References:**
- [GitHub REST API - Get team membership for a user](https://docs.github.com/fr/rest/teams/members?apiVersion=2022-11-28#get-team-membership-for-a-user)

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


```python
token = naas.secret.get("GITHUB_TOKEN") or "GITHUB_TOKEN"
org_id = "jupyter-naas"
team_id = "<team_id>"
username = "<username>"
```

## Model

### Get team membership for a user


```python
def get_team_membership(token, org, team, username):
    # Init
    res_json = None
    
    # Request
    url = f"https://api.github.com/orgs/{org}/teams/{team}/memberships/{username}"
    headers = {
        "Authorization": f"token {token}",
        "Accept": "application/vnd.github.hellcat-preview+json",
    }
    res = requests.get(url, headers=headers)
    
    # Result
    if res.status_code == 200:
        print(f"✅ User '{username }' found in '{org}/{team}'")
        res_json = res.json()
    else:
        print(f"❌ User not found in '{org}/{team}'")
    return res_json
```

## Output

### Display result


```python
membership = get_team_membership(token, org_id, team_id, username)
if membership:
    print(membership)
```

 
