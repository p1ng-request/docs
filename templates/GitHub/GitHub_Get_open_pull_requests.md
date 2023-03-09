<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_open_pull_requests.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+open+pull+requests:+Error+short+description">Bug report</a>

**Tags:** #github #repos #pulls #PR #operations #analytics #plotly #dataframe

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook retrieves pull requests from a repository URL.

**References:**
- [Get a pull request](https://docs.github.com/en/rest/pulls/pulls?apiVersion=2022-11-28#get-a-pull-request)

## Input

### Imports


```python
from naas_drivers import github
import naas
```

### Setup Variables
- `token`: [Generate a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `repository_url`: URL of your repository


```python
# GitHub token
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_TOKEN"

# Github repo on which we want to create issues.
repository_url = "ENTER_YOUR_REPO_URL_HERE"  # EXAMPLE : "https://github.com/jupyter-naas/awesome-notebooks"
```

## Model


```python
df_pulls = github.connect(token).repos.get_pulls(repository_url)
```

## Output

### Display result


```python
print("Opened PR:", len(df_pulls))
df_pulls
```
