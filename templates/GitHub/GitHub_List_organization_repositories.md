<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_organization_repositories.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+organization+repositories:+Error+short+description">Bug report</a>

**Tags:** #github #pygithub #list #organization #repositories

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to list organization repositories using pygithub.

**References:**
- [GitHub REST API v3](https://docs.github.com/fr/rest/repos/repos?apiVersion=2022-11-28#list-organization-repositories)
- [PyGithub Documentation](https://pygithub.readthedocs.io/en/latest/)

## Input

### Import libraries


```python
import github
```

### Setup Variables
- **token**: [Create a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)


```python
token = "YOUR_TOKEN"
```

## Model

### List organization repositories

Using the [PyGithub](https://pygithub.readthedocs.io/en/latest/) library, we can list all the repositories of an organization.


```python
# Create a Github instance
g = github.Github(token)
# Get the organization
org = g.get_organization("YOUR_ORGANIZATION")
# List all the repositories
repos = org.get_repos()
```

## Output

### Display result


```python
for repo in repos:
    print(repo.name)
```

 
