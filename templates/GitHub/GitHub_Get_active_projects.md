    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_active_projects.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+active+projects:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #projects #operations #snippet #dataframe

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook provides an overview of active projects on GitHub.

## Input

### Imports


```python
from naas_drivers import github
```

### Variables


```python
# Github project url
PROJECT_URL = "https://github.com/orgs/jupyter-naas/projects"

# Github token
GITHUB_TOKEN = "ghp_COJiJEU4cQR4rjslUjM9Duxxxxxx"
```

## Model


```python
df_projects = github.connect(GITHUB_TOKEN).projects.get(PROJECT_URL)
```

## Output

### Display result


```python
df_projects.head()
```
