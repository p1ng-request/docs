<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_files_added_on_pull_request.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+files+added+on+pull+request:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #pullrequest #files #merge #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook get the files added on a pull request using the GitHub API.

**References:**
- [GitHub API Documentation](https://developer.github.com/v3/)
- [GitHub Pull Request API Documentation](https://developer.github.com/v3/pulls/)

## Input

### Import libraries


```python
import requests
import naas
```

### Setup Variables
- `token`: Create your personal access token [here](https://github.com/settings/tokens)
- `owner`: owner of the repository
- `repo`: name of the repository
- `pull_number`: number of the pull request
- `file_status`: file types to be extracted: "added", "removed", "renamed"


```python
token = naas.secret.get("GITHUB_TOKEN") or "GITHUB_TOKEN"
owner = "jupyter-naas"
repo = "awesome-notebooks"
pull_number = 1496
file_status = "added"
```

## Model

### Get files added on pull request


```python
def get_files_added_on_pull_request(owner, repo, pull_number, file_status):
    files = []
    url = f"https://api.github.com/repos/{owner}/{repo}/pulls/{pull_number}/files"
    response = requests.get(url)
    files_changed = response.json()
    for file in files_changed:
        filename = file["filename"]
        status = file["status"]
        if status == file_status:
            files.append(filename)
    return files

files_added = get_files_added_on_pull_request(owner, repo, pull_number, file_status)
```

## Output

### Display result


```python
if len(files_added) > 0:
    for file in files_added:
        print("File added:", file)
```
