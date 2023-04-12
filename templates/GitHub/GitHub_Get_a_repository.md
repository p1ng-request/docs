    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_a_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+a+repository:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #pygithub #repository #get #rest #api

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get a repository using pygithub.

**References:**
- [GitHub - Get a repository](https://docs.github.com/fr/rest/repos/repos?apiVersion=2022-11-28#get-a-repository)

## Input

### Import libraries


```python
import naas
import github
```

### Setup Variables
- `token`: [Generate a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `repository_url`: URL of your repository


```python
token = naas.secret.get('GITHUB_TOKEN') or "YOUR_TOKEN"
repository_url = "https://github.com/jupyter-naas/awesome-notebooks"
```

## Model

### Get a repository


```python
# Create a Github instance
g = github.Github(token)
# Get a repository
repo = g.get_repo(repository_url.split("https://github.com/")[-1])
```

## Output

### Display result
Response attributes available here: https://docs.github.com/fr/rest/repos/repos?apiVersion=2022-11-28#get-a-repository


```python
print(repo)
```

 
