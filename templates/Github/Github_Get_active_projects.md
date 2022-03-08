<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_active_projects.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

The objective of the notebook is provide a list of active projects that an organization is working on

**Tags:** #github #projects

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

## Input

### Imports


```python
import requests
import pandas as pd
from urllib.parse import urlencode
from datetime import datetime
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
def get_active_project_links(token, url):
    project_df = pd.DataFrame()
    headers={"Authorization":f'token {token}'}
    url = "api.github.com".join(url.split("github.com"))
    page=1
    while True:
        params = {
            "per_page": 100,
            'page': page
        }
        url_link = url+ f"?{urlencode(params, safe='(),')}"
        res = requests.get(url_link, headers=headers, params=params)
        
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        if len(res.json()) == 0:
            break
        res_json = res.json()

        for idx, project in enumerate(res_json):
            project_df.loc[idx, 'project_name'] = project.get('name')
            project_df.loc[idx, 'project_description'] = project.get('body')
            project_df.loc[idx, 'project_id'] = project.get('number')
            project_df.loc[idx, 'project_created_by'] = project.get('creator')['login']
            
            project_df.loc[idx, 'project_created_date'] = project.get('created_at').strip('Z').split('T')[0]
            project_df.loc[idx, 'project_created_time'] = project.get('created_at').strip('Z').split('T')[-1]
            project_df.loc[idx, 'project_updated_date'] = project.get('updated_at').strip('Z').split('T')[0]
            project_df.loc[idx, 'project_updated_time'] = project.get('updated_at').strip('Z').split('T')[-1]
            
            project_df.loc[idx, 'project_columns_url'] = project.get('columns_url')
            
        page+=1
        
    project_df['project_id'] = project_df.project_id.astype('int')
    return project_df

df_projects = get_active_project_links(GITHUB_TOKEN, PROJECT_URL)
```

## Output

### Display result


```python
df_projects.head()
```
