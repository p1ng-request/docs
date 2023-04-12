<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Create_pull_request.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Create+pull+request:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #pygithub #pullrequest #create #assign #issue

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates a pull request using pygithub library.

**References:**
- [PyGithub Documentation](https://pygithub.readthedocs.io/en/latest/)
- [GitHub Documentation](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request)

## Input

### Import libraries


```python
try:
    import github
except:
    !pip install pygithub --user
    import github
import naas
```

### Setup Variables
- `token`: [GitHub token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `repo`: repository name
- `owner`: repository owner
- `title`: pull request title
- `body`: pull request body
- `head`: branch name where your changes are implemented
- `base`: branch name where your changes will be merged into


```python
token = naas.secret.get('GITHUB_TOKEN') or "YOUR_TOKEN"
repo = "YOUR_REPO"
owner = "YOUR_OWNER"
title = "YOUR_TITLE"
body = "YOUR_BODY" #To link your PR to an issue, you can add the following in your body 'This PR resolves {issue_html_url}'
head = "YOUR_HEAD"
base = "YOUR_BASE"
```

## Model

### Create Pull Request

Create a pull request with assignee and link to issue using pygithub library.


```python
# Create a Github instance
gh = github.Github(token)
# Get the repository
repo = gh.get_repo(f"{owner}/{repo}")
# Create the pull request
pull_request = repo.create_pull(
    title=title, body=body, head=head, base=base
)
```

## Output

### Display result


```python
# Display the pull request
pull_request
```

 
