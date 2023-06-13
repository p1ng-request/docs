<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Remove_team_membership_for_a_user.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Remove+team+membership+for+a+user:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #teams #members #remove #api #rest

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to remove team membership for a user. It is usefull for organizations that need to manage their team memberships.

**References:**
- [GitHub REST API Documentation](https://docs.github.com/fr/rest/teams/members?apiVersion=2022-11-28#remove-team-membership-for-a-user)
- [GitHub API Authentication](https://docs.github.com/en/developers/apps/authorizing-oauth-apps)

## Input

### Import libraries


```python
import requests
import json
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
```

## Model

### Remove team membership for a user


```python
def remove_team_membership(token, org, team, username):
    # Init
    res_json = None
    
    # Request
    url = f"https://api.github.com/orgs/{org}/teams/{team}/memberships/{username}"
    headers = {"Authorization": f"token {token}"}
    res = requests.delete(url, headers=headers)
    return res
```

## Output

### Display result


```python
response = remove_team_membership(token, org_id, team_id, username)
print(response.status_code)
print(response.text)
```
