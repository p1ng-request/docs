<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_branches.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+branches:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #branches #list #api #rest #python

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will list all branches from a given GitHub repository;

**References:**
- [GitHub - List branches](https://docs.github.com/en/rest/branches/branches?apiVersion=2022-11-28#list-branches)
- [GitHub - Authentication](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#authentication)

## Input

### Import libraries


```python
import naas
import pandas as pd
try:
    from github import Github
except:
    !pip install PyGithub --user
    from github import Github
from pprint import pprint
```

### Setup Variables
- `token`: [Generate a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `owner`: owner of the repository
- `repository`: name of the repository


```python
token = naas.secret.get(name="GITHUB_TOKEN") or "YOUR_GITHUB_TOKEN"
owner = "jupyter-naas" #This is an example for naas
repository = "awesome-notebooks" #This is an example for naas
```

## Model

### List branches


```python
def list_branches(owner, repository):
    g = Github(token)

    try:
        repo = g.get_repo(f"{owner}/{repository}")
        branches = repo.get_branches()

        data = []
        for branch in branches:
            branch_data = {
                'branch': branch.name,
                'creation_date': branch.commit.commit.author.date,
                'creator': branch.commit.commit.author.name
            }
            data.append(branch_data)

        df = pd.DataFrame(data)
        return df

    except Exception as e:
        print(f"An error occurred: {e}")
        return pd.DataFrame()

branches_df = list_branches(owner, repository)
```

## Output

### Display result


```python
print(f"Branches for {owner}/{repository}:", len(branches_df))
print("-" * 50)
pprint(branches_df['branch'].tolist())
print("-" * 50)
```

 
