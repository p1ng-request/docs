<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Create_issue.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #github #productivity #code

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

## Input

### Import library


```python
from github import Github
```

### Enter repository path and token


```python
repo_name = "**********"                                           # Repository path
git_key = "**********"                                             # Settings/Developer settings
assignee = "**********"                                            # Asignee name (optional) or put ""
issue_title = "This is a another issue"                            # Issue title
issue_description = "This is another issue body created using api" # Issue description
```

## Model

### Establishing connection


```python
g = Github(git_key)   
```

## Output

### Creating github issue with assignee


```python
repo = g.get_repo(repo_name)
repo.create_issue(title = issue_title, body = issue_description, assignee = assignee)
```
