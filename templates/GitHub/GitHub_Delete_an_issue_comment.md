<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Delete_an_issue_comment.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Delete+an+issue+comment:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #issue #comment #api #python #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to delete a comment to an issue on GitHub.

**References:**
- [GitHub API Documentation](https://docs.github.com/fr/rest/issues/comments?apiVersion=2022-11-28#delete-an-issue-comment)

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
- `comment_id`: Id of comment to be deleted. To find it, you can use "GitHub - List issue comments"


```python
token = naas.secret.get('GITHUB_TOKEN')
owner = "jupyter-naas"
repo = "awesome-notebooks"
comment_id = 1563983688
```

## Model

### Delete an issue comment


```python
def delete_issue_comment(
    token=None,
    owner=None,
    repo=None,
    comment_id=None
):  
    # URL
    url = f"https://api.github.com/repos/{owner}/{repo}/issues/comments/{comment_id}"

    # Set the request headers
    headers = {
        "Authorization": f"token {token}",
        "Content-Type": "application/json"
    }
    # Send the POST request
    res = requests.delete(url, headers=headers)
    if res.status_code == 204:
        print(f"✅ Comment deleted on issue")
        return res
    else:
        print(res.status_code, res.json())
```

## Output

### Display result


```python
delete_issue_comment(token, owner, repo, comment_id)
```

 
