<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_List_issue_comments.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+List+issue+comments:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #issue #comment #api #python #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to list comments from an issue on GitHub.

**References:**
- [GitHub API Documentation](https://docs.github.com/fr/rest/issues/comments?apiVersion=2022-11-28#list-issue-comments)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Variables
- `token`: [GitHub token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)
- `owner`: owner of the repository
- `repo`: name of the repository
- `issue_number`: number of the issue


```python
token = naas.secret.get('GITHUB_TOKEN')
owner = "jupyter-naas"
repo = "awesome-notebooks"
issue_number = 1808
```

## Model

### Flatten nested dict


```python
# Flatten the nested dict
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)
```

### Create an issue comment


```python
def list_issue_comments(
    token=None,
    owner=None,
    repo=None,
    issue_number=None,
):
    # Init
    page = 1
    df = pd.DataFrame()
    while True:
        url = f"https://api.github.com/repos/{owner}/{repo}/issues/{issue_number}/comments?per_page=100&page={page}"
        response = requests.get(url)
        headers = {"Authorization": f"token {token}"}
        res = requests.get(url, headers=headers)
        if res.status_code == 200 and len(res.json()) > 0:
            res_json = res.json()
            for r in res_json:
                flatten_r = flatten_dict(r)
                tmp_df = pd.DataFrame([flatten_r])
                df = pd.concat([df, tmp_df]).sort_values("created_at")
            page += 1
        else:
            break
    return df
```

## Output

### Display result


```python
df = list_issue_comments(token, owner, repo, issue_number)
print('Comments fetched:', len(df))
print(df.info())
df
```

 
