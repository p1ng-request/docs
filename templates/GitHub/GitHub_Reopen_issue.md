<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Reopen_issue.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Reopen+issue:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #issues #update #rest #api #snippet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook explains how to reopened an issue on GitHub using the REST API.

**References:**
- [GitHub REST API Documentation](https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#update-an-issue)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `token`: [GitHub token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)
- `owner`: owner of the repository
- `repo`: name of the repository
- `issue_number`: number of the issue


```python
# Inputs
token = naas.secret.get('GITHUB_TOKEN')
owner = "jupyter-naas"
repo = "awesome-notebooks"
issue_number = 99
```

## Model

### Update issue

This function updates an issue on GitHub using the REST API.


```python
def update_issue(
    token,
    owner,
    repo,
    issue_number,
    title=None,
    body=None,
    state="open",
    state_reason="reopened",
    labels=[],
    assignees=[],
):
    url = f"https://api.github.com/repos/{owner}/{repo}/issues/{issue_number}"
    headers = {"Authorization": f"token {token}"}
    data = {}
    if title:
        data["title"] = title
    if body:
        data["body"] = body
    if state:
        data["state"] = state
    if state_reason:
        data["state_reason"] = state_reason
    if len(labels) > 0:
        data["labels"] = labels
    if len(assignees) > 0:
        data["assignees"] = assignees
    
    # Send the PATCH request
    res = requests.patch(url, headers=headers, json=data)
    if res.status_code == 200:
        print(f"✅ Issue reopened:", f"https://github.com/{owner}/{repo}/issues/{issue_number}")
        return res
    else:
        print(res.status_code, res.json())
```

## Output

### Display Result


```python
update_issue(
    token,
    owner,
    repo,
    issue_number,
)
```

 
