<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_commits_from_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+commits+from+repository:+Error+short+description">Bug report</a>

**Tags:** #github #repos #commits #stats #naas_drivers #plotly #linechart #operations #analytics #dataframe #html

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides a tutorial on how to retrieve a list of commits for a specific repository on GitHub using the GitHub API. It covers how to set up a personal access token for accessing the API, how to get commits using naas_drivers.github. The output returned is a dataframe.

## Input

### Import libraries


```python
from naas_drivers import github
from datetime import datetime
import naas
```

### Setup GitHub
**How to find your personal access token on Github?**
- First we need to create a personal access token to get the details of our organization from here: https://github.com/settings/tokens
- You will be asked to select scopes for the token. Which scopes you choose will determine what information and actions you will be able to perform against the API.
- You should be careful with the ones prefixed with write:, delete: and admin: as these might be quite destructive.
- You can find description of each scope in docs here (https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps).


```python
# Inputs
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"  # Github repository url
GITHUB_TOKEN = (
    naas.secret.get("GITHUB_TOKEN") or "ghp_CEvqR7QauDbNLRiIiwAC1v4xxxxxxxxxxxxx"
)  # Github token

# Outputs
repository_name = REPO_URL.split("/")[-1]
timestamp = datetime.now().strftime("%Y%m%s%H%M%S")
csv_path = (
    f"{timestamp}_{repository_name}.csv"  # returned the name of the repository as csv
)
```

## Model

### Get commits from repository url


```python
df_commits = github.connect(GITHUB_TOKEN).repos.get_commits(REPO_URL)
df_commits
```

## Output

### Save dataframe in CSV


```python
df_commits.to_csv(csv_path, index=False)
```
