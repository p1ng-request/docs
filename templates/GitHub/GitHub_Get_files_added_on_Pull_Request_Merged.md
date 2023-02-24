<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_files_added_on_Pull_Request_Merged.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+files+added+on+Pull+Request+Merged:+Error+short+description">Bug report</a>

**Tags:** #github #pullrequest #files #merge #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get the files added on a Pull Request Merged using the GitHub API.

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


```python
token = naas.secret.get("GITHUB_TOKEN") or "GITHUB_TOKEN"
owner = "jupyter-naas"
repo = "awesome-notebooks"
pull_number = 1496
```

## Model

### Get files added on Pull Request Merged


```python
# Get the files added on the Pull Request Merged
url = f"https://api.github.com/repos/{owner}/{repo}/pulls/{pull_number}/files"
response = requests.get(url)
files = response.json()
```

## Output

### Display result


```python
# Display the files added on the Pull Request Merged
for file in files:
    print(file["filename"])
```
