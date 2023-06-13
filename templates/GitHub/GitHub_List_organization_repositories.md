<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_organization_repositories.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+organization+repositories:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #pygithub #list #organization #repositories

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to list organization repositories using pygithub.

**References:**
- [GitHub REST API v3](https://docs.github.com/fr/rest/repos/repos?apiVersion=2022-11-28#list-organization-repositories)
- [PyGithub Documentation](https://pygithub.readthedocs.io/en/latest/)

## Input

### Import libraries


```python
import naas
import github
```

### Setup Variables
- `token`: [Create a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `organization`: name of your github organization


```python
token = naas.secret.get('GITHUB_TOKEN') or "YOUR_TOKEN"
organization = "jupyter-naas"
```

## Model

### List organization repositories

Using the [PyGithub](https://pygithub.readthedocs.io/en/latest/) library, we can list all the repositories of an organization.


```python
# Create a Github instance
g = github.Github(token)
# Get the organization
org = g.get_organization(organization)
# List all the repositories
repos = org.get_repos()
```

## Output

### Display result
Response attributes available here: https://docs.github.com/fr/rest/repos/repos?apiVersion=2022-11-28#get-a-repository


```python
for repo in repos:
    print(repo.name)
```

 
