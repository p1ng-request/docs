<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_pull_requests_from_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

The objective of this notebook is to maintain a track of open pull requests that have been pending a review since more than 7 days within a repository

**Tags:** #github #repos #pulls #PR

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

## Input

### Imports


```python
import requests
import pandas as pd
from urllib.parse import urlencode
from datetime import datetime
import plotly.express as px
```

### Variables


```python
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"
GITHUB_TOKEN = "ghp_COJiJEU4cQR4rjslUjM9DupYFswxxxxxxxxxxxxxxxxx"
```

## Model


```python
def get_pulls_from_repo(token, repo_url):
    repository = repo_url.split("https://github.com/")[-1]
    headers = {'Authorization': f'token {token}'}
    df = pd.DataFrame()
    page = 1
    while True:
        params = {
            "per_page": "100",
            "page": page,
        }
        url = f"https://api.github.com/repos/{repository}/pulls?{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        res_json = res.json()
        if len(res_json) == 0:
            break
        
        for idx, r in enumerate(res_json):
            if r.get('state') == 'open':
                df.loc[idx, 'id'] = r.get('id')
                df.loc[idx, 'issue_url'] = r.get('issue_url')
                df.loc[idx, 'PR_number'] = r.get('number')
                df.loc[idx, 'PR_state'] = 'open'
                df.loc[idx, 'Title'] = r.get('title')
                
                df.loc[idx, 'first_created_date'] = r.get('created_at').strip('Z').split('T')[0]
                df.loc[idx, 'first_created_time'] = r.get('created_at').strip('Z').split('T')[-1]
                df.loc[idx, 'last_updated_date'] = r.get('updated_at').strip('Z').split('T')[0]
                df.loc[idx, 'last_updated_time'] = r.get('updated_at').strip('Z').split('T')[-1]
                
                df.loc[idx, 'commits_url'] = r.get('commits_url')
                df.loc[idx, 'review_comments_url'] = r.get('review_comments_url')
                df.loc[idx, 'issue_comments_url'] = r.get('comments_url')
                
                assignees_lst, reviewers_lst=[],[]
                for assignee in r.get('assignees'):
                    assignees_lst.append(assignee.get('login'))
                for reviewer in r.get('requested_reviewers'):
                    reviewers_lst.append(reviewer.get('login'))
                
                if assignees_lst==[]:
                    df.loc[idx, 'assignees'] = 'None'
                elif assignees_lst:
                    df.loc[idx, 'assignees'] = ", ".join(assignees_lst)
                    
                if reviewers_lst==[]:
                    df.loc[idx, 'requested_reviewers'] = 'None'
                elif reviewers_lst:
                    df.loc[idx, 'requested_reviewers'] = ", ".join(reviewers_lst)
                    
                date_format = "%Y-%m-%d"
                delta = datetime.now() - datetime.strptime(df.loc[idx, 'last_updated_date'], date_format)
                df.loc[idx, 'PR_activity'] = f'No activity since {delta.days} days'
                
            df['PR_number'] = df.PR_number.astype('int')
            df.id = df.id.astype('int')

        page+=1
        
    return df

df_pulls = get_pulls_from_repo(GITHUB_TOKEN, REPO_URL)
```

## Output

### Display result


```python
print("Opened PR:", len(df_pulls))
df_pulls
```
