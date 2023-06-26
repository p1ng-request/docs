<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_branches_with_open_PR.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+branches+with+open+PR:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #branches #list #api #rest #python #active

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will list branches with open PR from a given GitHub repository.

**References:**
- [GitHub - List branches](https://docs.github.com/en/rest/branches/branches?apiVersion=2022-11-28#list-branches)
- [GitHub - Authentication](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#authentication)

## Input

### Import libraries


```python
import naas
import pandas as pd
import requests
from pprint import pprint
```

### Setup Variables
- `token`: [Generate a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `owner`: owner of the repository
- `repository`: name of the repository


```python
token = naas.secret.get(name="GITHUB_TOKEN") or "YOUR_GITHUB_TOKEN"
owner = "jupyter-naas" #Example for naas
repository = "awesome-notebooks" #Example for naas awesome-notebooks repository
```

## Model

### List branches with open PR's

This function will list get active branches, creator and Creation date from a given GitHub repository.


```python
def get_branches_with_open_prs(
    token,
    owner,
    repository
):
    url = f"https://api.github.com/repos/{owner}/{repository}/pulls"
    headers = {"Authorization": f"token {token}"}
    response = requests.get(url, headers=headers)
    pulls = response.json()
    
    branches_data = []
    
    for pull in pulls:
        branch = pull['head']['ref']
        creator = pull['user']['login']
        creation_date = pull['created_at']
        
        branches_data.append({
            'branch': branch,
            'creator': creator,
            'creation_date': creation_date
        })
    
    branches_df = pd.DataFrame(branches_data)
    return branches_df

branches_with_open_prs = get_branches_with_open_prs(token, owner, repository)
```

## Output

### Display result


```python
print(f"Branches with open pull requests in {owner}/{repository}:", len(branches_with_open_prs))
print("-" * 70)
pprint(branches_with_open_prs['branch'].tolist())
print("-" * 70)
```

 
