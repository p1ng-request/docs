<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Github - Get issues from repo
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_issues_from_repo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

The objective of the notebook is to maintain a track of issues that are open in a particular repository

**Tags:** #github #repos #issues

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
# Github repository url
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"

# Github token
GITHUB_TOKEN = "ghp_COJiJEU4cQR4rjslUxxxxxxxxxxxxxxxx"
```

## Model

### Get comments from issues function


```python
def get_comments_from_issues(token, url):
    headers={"Authorization":f'token {token}'}
    issue_comments=[]
    
    if url.find("api.github.com")==-1:
        url = "api.github.com".join(url.split("github.com"))
    
    comments = requests.get(url, headers=headers)
    try:
        comments.raise_for_status()
    except requests.HTTPError as e:
        raise(e)
    if len(comments.json())==0:
        return 'No comments'
    else:
        for comment in comments.json():
            issue_comments.append(comment['body'])
    return issue_comments
```

### Get issues from repo


```python
def get_issues_from_repo(token, repo_url):
    repository = repo_url.split("https://github.com/")[-1]
    headers = {'Authorization': f'token {token}'}
    df = pd.DataFrame()
    page = 1
    while True:
        params = {
            "per_page": "100",
            "page": page,
        }
        url = f"https://api.github.com/repos/{repository}/issues?{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        res_json = res.json()
        if len(res_json) == 0:
            break
        
        for idx, issue in enumerate(res_json):
            df.loc[idx, 'link_to_the_issue'], df.loc[idx, 'issue_number'] = issue['html_url'], issue['number']
            df.loc[idx, 'issue_title'], df.loc[idx, 'issue_state'] = issue['title'], issue['state']
            df.loc[idx, 'issue_id'] = issue['id']
            labels= []
            for label in issue['labels']:
                labels.append(label.get('name'))
            if labels==[]:
                df.loc[idx, 'issue_labels'] = 'None'
            else:
                df.loc[idx, 'issue_labels'] = ", ".join(labels)

            assigned=[]
            for assignee in issue['assignees']:
                assigned.append(assignee.get('login'))
            if assigned==[]:
                df.loc[idx, 'issue_assignees'] = 'None'
            else:
                df.loc[idx, 'issue_assignees'] = ", ".join(assigned)

            df.loc[idx, 'comments_till_date'] = issue['comments']
            
            df.loc[idx, 'last_created_date'] = issue.get('created_at').strip('Z').split('T')[0]
            df.loc[idx, 'last_created_time'] = issue.get('created_at').strip('Z').split('T')[-1]
            df.loc[idx, 'last_updated_date'] = issue.get('updated_at').strip('Z').split('T')[0]
            df.loc[idx, 'last_updated_time'] = issue.get('updated_at').strip('Z').split('T')[-1]
        
            df.loc[idx, 'comments'] = str(get_comments_from_issues(token, issue['comments_url']))
            
            try:
                pr = requests.get(issue.get('pull_request')['url'], headers= headers).json()
                df.loc[idx, 'linked_pr_state'] = pr.get('state')
                
                date_format = "%Y-%m-%d"
                delta = datetime.now() - datetime.strptime(df.loc[idx, 'last_updated_date'], date_format)
                df.loc[idx, 'PR_activity'] = f'No activity since {delta.days} days'
                
            except:
                df.loc[idx, 'linked_pr_state'] = 'None'
                df.loc[idx, 'PR_activity'] = 'None'
        page+=1
        
    df['issue_id'] = df.issue_id.astype('int')
    df['comments_till_date'] = df.comments_till_date.astype('int')
    df['issue_number'] = df.issue_number.astype('int')

    return df

df_issues = get_issues_from_repo(GITHUB_TOKEN, REPO_URL)
```

## Output

### Display result


```python
print("Nb issues:", len(df_issues))
df_issues.head(15)
```
