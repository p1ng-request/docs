<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Create_an_issue_comment.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Create+an+issue+comment:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #issue #comment #api #python #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to add a comment to an issue on GitHub.

**References:**
- [GitHub API Documentation](https://docs.github.com/en/rest/issues/comments?apiVersion=2022-11-28#create-an-issue-comment)

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
- `comment`: comment to be added


```python
token = naas.secret.get('GITHUB_TOKEN')
owner = "jupyter-naas"
repo = "awesome-notebooks"
issue_number = 1808
comment = "This is a comment"
```

## Model

### Create an issue comment


```python
def create_issue_comment(
    token=None,
    owner=None,
    repo=None,
    issue_number=None,
    comment=None
):  
    # URL
    url = f"https://api.github.com/repos/{owner}/{repo}/issues/{issue_number}/comments"
    data = {"body": comment}

    # Set the request headers
    headers = {
        "Authorization": f"token {token}",
        "Content-Type": "application/json"
    }
    # Send the POST request
    res = requests.post(url, headers=headers, json=data)
    if res.status_code == 201:
        print(f"✅ Comment added on issue:", f"https://github.com/{owner}/{repo}/issues/{issue_number}")
        return res
    else:
        print(res.status_code, res.json())
```

## Output

### Display result


```python
create_issue_comment(token, owner, repo, issue_number, comment)
```

 
