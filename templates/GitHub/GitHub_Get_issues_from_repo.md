<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_issues_from_repo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+issues+from+repo:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #repos #issues #operations #analytics #dataframe #html #plotly

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook allows users to retrieve issues from a GitHub repository.

## Input

### Imports


```python
from naas_drivers import github
```

### Variables


```python
# Github repository url
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"

# Github token
GITHUB_TOKEN = "ghp_COJiJEU4cQR4rjslUxxxxxxxxxxxxxxxx"
```

## Model

### Get issues from repo


```python
df_issues = github.connect(GITHUB_TOKEN).repos.get_issues(REPO_URL)
```

## Output

### Display result


```python
print("Nb issues:", len(df_issues))
df_issues.head(15)
```
