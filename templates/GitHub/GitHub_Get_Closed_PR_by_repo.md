<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_Closed_PR_by_repo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+Closed+PR+by+repo:+Error+short+description">Bug report</a>

**Tags:** #github #pygithub #closedpr #repo #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get closed PR by repo using pygithub library.

**References:**
- [PyGithub Documentation](https://pygithub.readthedocs.io/en/latest/)
- [GitHub API Documentation](https://developer.github.com/v3/)

## Input

### Import libraries


```python
import os
import json
from github import Github
import naas
```

### Setup Variables
- `token`: [GitHub token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)
- `repo_name`: name of the repository


```python
token = naas.secret.get("GITHUB_TOKEN") or os.environ.get("GITHUB_TOKEN")
repo_name = "jupyter-naas/awesome-notebooks"
```

## Model

### Get Closed PR by repo

Using the `Github` class from the `github` library, we can connect to the GitHub API and get the closed PR from a given repository.


```python
# Connect to the GitHub API
g = Github(token)
# Get the repository
repo = g.get_repo(repo_name)
# Get the closed PR
closed_pr = repo.get_pulls(state="closed")
```

## Output

### Display result


```python
# Print the closed PR
for pr in closed_pr:
    print(json.dumps(pr.raw_data, indent=4))
```

 
