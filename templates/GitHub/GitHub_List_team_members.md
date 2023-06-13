<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_team_members.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+team+members:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #teams #members #rest #api #list #snippet

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will demonstrate how to list team members using the GitHub REST API and will create a DataFrame as output. It can be used by organizations or repository owners to manage their teams on GitHub by listing the current team members. It helps in keeping track of team members, their roles, and permissions, enabling organizations to efficiently manage their teams and ensure that the right users have the appropriate access.

DataFrame returned:
- login': Represents the username or login name of the GitHub user.
- 'id': Represents the unique identifier assigned to the GitHub user.
- 'node_id': Represents the unique identifier for the GitHub user's profile as a node in the GitHub GraphQL API.
- 'avatar_url': Represents the URL of the avatar (profile picture) of the GitHub user.
- 'gravatar_id': Represents the unique identifier associated with the GitHub user's Gravatar profile.
- 'url': Represents the URL of the GitHub user's profile.
- 'html_url': Represents the HTML URL of the GitHub user's profile.
- 'followers_url': Represents the URL for retrieving the list of followers of the GitHub user.
- 'following_url': Represents the URL for retrieving the list of users that the GitHub user is following.
- 'gists_url': Represents the URL for retrieving the list of gists created by the GitHub user.
- 'starred_url': Represents the URL for retrieving the list of repositories starred by the GitHub user.
- 'subscriptions_url': Represents the URL for retrieving the list of repositories subscribed to by the GitHub user.
- 'organizations_url': Represents the URL for retrieving the list of organizations the GitHub user is a member of.
- 'repos_url': Represents the URL for retrieving the list of repositories owned by the GitHub user.
- 'events_url': Represents the URL for retrieving the list of events related to the GitHub user's activity.
- 'received_events_url': Represents the URL for retrieving the list of events received by the GitHub user.
- 'type': Represents the type of GitHub user, which can be 'User' or 'Organization'.
- 'site_admin': Represents a boolean value indicating if the GitHub user has administrative privileges (true) or not (false) in the associated organization or repository.

**References:**
- [List team members](https://docs.github.com/fr/rest/teams/members?apiVersion=2022-11-28#list-team-members)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Variables
- `token`: Create your personal access token [here](https://github.com/settings/tokens)
- `team_url`: The URL of the team to list pending invitations for.


```python
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_TOKEN"
team_url = "https://github.com/orgs/jupyter-naas/teams/opensource-contributors"
```

## Model

### List team members
This action will list all members of a team using the GitHub REST API.


```python
def list_team_members(team_url, token):
    # Init
    page = 1
    df_members = pd.DataFrame()
    org = team_url.split("/orgs/")[-1].split("/")[0]
    team_slug = team_url.split("/teams/")[-1]
    while True:
        url = f"https://api.github.com/orgs/{org}/teams/{team_slug}/members?per_page=100&page={page}"
        response = requests.get(url)
        headers = {"Authorization": f"token {token}"}
        res = requests.get(url, headers=headers)
        if res.status_code == 200 and len(res.json()) > 0:
            df = pd.DataFrame(res.json())
            df_members = pd.concat([df_members, df])
            page += 1
        else:
            break
    return df_members

df_team_members = list_team_members(team_url, token)
```

## Output

### Display result


```python
print("Team members found:", len(df_team_members))
df_team_members
```

 
