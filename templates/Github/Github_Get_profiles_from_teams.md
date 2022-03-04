#### <img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Github - Get profiles from teams
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_profiles_from_teams.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook enables you to get a dataframe of all the team members in a Github organization.

**Tags:** #github #team

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

## Input

### Import libraries


```python
import pandas as pd
import requests
import naas
from urllib.parse import urlencode
```

### Setup Github

**How to find your personal access token on Github?** 
- First we need to create a personal access token to get the details of our organization from here: https://github.com/settings/tokens
- You will be asked to select scopes for the token. Which scopes you choose will determine what information and actions you will be able to perform against the API. 
- You should be careful with the ones prefixed with write:, delete: and admin: as these might be quite destructive. 
- You can find description of each scope in docs here (https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps).


### Variables


```python
TEAM_URL = "https://github.com/orgs/jupyter-naas/teams"
GITHUB_TOKEN = "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"
```

## Model


```python
####### Traverses through multiple teams and all member profiles within each team #########

def get_profiles_from_teams(token, url):
    org = url.split("https://github.com/orgs/")[-1].split("/")[0]
    headers = {'Authorization': f'token {token}'}
    member_profiles, teams, slugs, team_descriptions=[],[],[],[]
    data = pd.DataFrame(columns=['TEAM', 'SLUG','TEAM_DESCRIPTION', 'member_profile','GITHUB'])
    page = 1
    
    while True:
        params = {
            "state": "open",
            "per_page": "100",
            "page": page,
        }
        url = f"https://api.github.com/orgs/{org}/teams?{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        res_json = res.json()

        if len(res_json) == 0:
            break
        
        members_details=[]
        for team_info in res_json:
            members_details.append((team_info['name'], team_info['slug'], team_info['description'], team_info['members_url'].strip("{/member}")))
        
        
        for info in members_details:
            page_number=1
            while True:
                members_params ={
                    "state": "open",
                    "per_page": "100",
                    "page": page_number,
                }
                
                url = f"{info[3]}?{urlencode(members_params, safe='(),')}"
                members = requests.get(url, headers=headers, params=members_params)
                
                try:
                    members.raise_for_status()
                except requests.HTTPError as e:
                    raise(e)
                members_json = members.json()

                if len(members_json) == 0:
                    break
                
                for member in members_json:
                    member_profiles.append(member['url'])
                    teams.append(info[0])
                    slugs.append(info[1])
                    team_descriptions.append(info[2])
                
                page_number+=1
        
        page += 1
    
    data['TEAM'], data['SLUG'], data['TEAM_DESCRIPTION'], data['member_profile'] = teams, slugs, team_descriptions, member_profiles     
    data['GITHUB'] = org

    for idx, profile in enumerate(data['member_profile']):
        details = requests.get(profile, headers=headers, params= params).json()
        data.loc[idx,'NAME'], data.loc[idx,'EMAIL'], data.loc[idx,'LOCATION'] = details['name'], details['email'], details['location']
        data.loc[idx,'ORGANIZATION'], data.loc[idx,'BIO'], data.loc[idx,'LOGIN_NAME'] = details['company'], details['bio'], details['login']
        data.loc[idx,'TWITTER'], data.loc[idx,'CREATED_AT'], data.loc[idx,'UPDATED_AT'] = details['twitter_username'], details['created_at'], details['updated_at']    
        
    return data

df_teams = get_profiles_from_teams(GITHUB_TOKEN, TEAM_URL)
```

## Output


```python
print(f'Dataset size -> {df_teams.shape}')
df_teams.head(25)
```


```python

```
