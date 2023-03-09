<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_closed_pull_requests.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+closed+pull+requests:+Error+short+description">Bug report</a>

**Tags:** #github #pygithub #closedpr #repo #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook list closed pull requests from a repository name using pygithub library.

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
- `token`: [Generate a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `repo_name`: name of the repository


```python
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_TOKEN"
repo_name = "jupyter-naas/awesome-notebooks"
```

## Model

### List pull requests

Using the `Github` class from the `github` library, we can connect to the GitHub API and get the closed PR from a given repository.


```python
# Connect to the GitHub API
g = Github(token)
# Get the repository
repo = g.get_repo(repo_name)
# Get the closed PR
pull_requests = repo.get_pulls(state="closed")
```

## Output

### Display result


```python
# Print the closed PR
print("✅ Pull Requests fetched:", pull_requests.totalCount)
for index, pr in enumerate(pull_requests):
    print(json.dumps(pr.raw_data, indent=4))
    break
```

 
