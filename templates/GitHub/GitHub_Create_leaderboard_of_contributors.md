    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Create_leaderboard_of_contributors.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Create+leaderboard+of+contributors:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #repos #commits #stats #naas_drivers #leaderboard #commitsPoints

**Author:** [Suhas B](https://www.linkedin.com/in/suhasbrao/)


## Input

### Import libraries


```python
import pandas as pd
import plotly.express as px
from naas_drivers import github
import naas

import requests
from urllib.parse import urlencode
```

## Setup Github
**How to find your personal access token on Github?**

- First we need to create a personal access token to get the details of our organization from here: https://github.com/settings/tokens
- You will be asked to select scopes for the token. Which scopes you choose will determine what information and actions you will be able to perform against the API.
- You should be careful with the ones prefixed with write:, delete: and admin: as these might be quite destructive.
- You can find description of each scope in docs here (https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps).


```python
# Github repository url
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"

# Github token
GITHUB_TOKEN = naas.secret.get("Git_Token")
```

## Model

### Get actor/user who closed the issue


```python
# Function to get the actor for closing an issue
def get_actor_for_closed_issue(events_url, git_obj):
    '''
    This function is used to get actor for a closed issues
    It gives the name of a person who closed the issue.
    
    Parameters
    ----------
    events_url: str:
        events_url from Github.
        Example : "https://api.github.com/repos/jupyter-naas/awesome-notebooks/issues/1401/events"
    
    git_obj: object of naas_driver.github
    '''
    
    url = events_url
    res = requests.get(url, headers=git_obj.headers)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        raise(e)
    
    res_json = res.json()
    if len(res_json) == 0:
        return
    
    
    actor = None
    for events in res_json:
        if events["event"] == "closed":
            actor= events["actor"]["login"]
    
    return actor
# get_actor_for_closed_issue("https://api.github.com/repos/jupyter-naas/awesome-notebooks/issues/1392/events")
```

### Get All Issues (both open and closed issues)


```python
def get_all_issues(repo_url):
    '''
    This function retrives all the issues of a repository and returns a 
    dataframe with the following columns:
    
    link_to_the_issue
    issue_title
    issue_number
    issue_state
    issue_creator
    issue_closed_by
    last_created_date
    last_created_time
    last_updated_date
    last_updated_time
    

    Parameters
    ----------
    repo_url: str:
        Repository url from Github.
        Example : "https://github.com/jupyter-naas/awesome-notebooks"
    '''
    
    git_obj = github.connect(GITHUB_TOKEN)
    repository = git_obj.get_repository_url(repo_url)
    df = pd.DataFrame()
    page, idx = 1, 0
    while True:
        params = {
                "per_page": "100",
                "page": page,
            }
        
        # Api to get open issues from github
        url = f"https://api.github.com/repos/{repository}/issues?state=all&{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=git_obj.headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        
        res_json = res.json()
        if len(res_json) == 0:
            break
        
        for issue in res_json:
            # Fetch all the issues, check node_id to see if it is an issue or PR
            
            if(issue["node_id"].startswith("I_")):
                
                df.loc[idx,'link_to_the_issue'], df.loc[idx, 'issue_number'] = issue['html_url'], issue['number']
                df.loc[idx, 'issue_title'], df.loc[idx, 'issue_state'] = issue['title'], issue['state']
   
                df.loc[idx, "issue_creator"] = issue["user"].get("login")
                
                # Create a cloumn that stores the name of the person who closed the issue
                # else if the issue is Open the column value will be None
                df.loc[idx, "issue_closed_by"] = get_actor_for_closed_issue( issue["events_url"], git_obj )
                
                df.loc[idx, 'last_created_date'] = issue.get('created_at').strip('Z').split('T')[0]
                df.loc[idx, 'last_created_time'] = issue.get('created_at').strip('Z').split('T')[-1]
                df.loc[idx, 'last_updated_date'] = issue.get('updated_at').strip('Z').split('T')[0]
                df.loc[idx, 'last_updated_time'] = issue.get('updated_at').strip('Z').split('T')[-1]
                
                
                idx +=1
        page+=1
    return df


```

### Get Issue/PR comments


```python
def get_issue_pr_comments(repo_url):
    '''
    The function retrieves all the issue comments and pr comments for a given r
    repository url.
    The function returns a dataframe with following columns for an issue comment/pr comment
    
    comment_id
    issue_url
    comment_by
    comment_body
    '''
    git_obj = github.connect(GITHUB_TOKEN)
    repository = git_obj.get_repository_url(repo_url)
    df = pd.DataFrame()
    page, idx = 1, 0
    while True:
        params = {
                "per_page": "100",
                "page": page,
            }
        
        # Api to get comments from github
       
        url = f"https://api.github.com/repos/{repository}/issues/comments?{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=git_obj.headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        
        res_json = res.json()
        if len(res_json) == 0:
            break
        
        for issue_comment in res_json:
            df.loc[idx, "comment_id"] = issue_comment["id"]
            df.loc[idx, "issue_url"] = issue_comment["issue_url"]
            df.loc[idx, "comment_by"] = issue_comment["user"]["login"]
            df.loc[idx, "comment_body"] = issue_comment["body"]
            
            idx +=1
        page += 1
        
    return df
```

### Get Contributor Details


```python
def get_contributors_details(repo_url):
    '''
    The function retrieves contributors for a given repository url
    This function returns a dataframe of contributors with following columns
    
    contributor_name
    issues_created
    issues_closed
    issue_pr_comments
    commits
    
    '''
    git_obj = github.connect(GITHUB_TOKEN)
    repository = git_obj.get_repository_url(repo_url)
    df = pd.DataFrame()
    page, idx = 1, 0
    while True:
        params = {
                "per_page": "100",
                "page": page,
            }
        url = f"https://api.github.com/repos/{repository}/contributors?{urlencode(params, safe='(),')}"
        res = requests.get(url, headers=git_obj.headers)
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        
        res_json = res.json()
        if len(res_json) == 0:
            break
        
        for contributor in res_json:
            df.loc[idx, "contributor_name"] = contributor["login"]
            # create a column to store number of issues created by a contributor
            df.loc[idx, "issues_created"] = len(df_all_issues.loc[df_all_issues["issue_creator"]==contributor["login"]])
            # create a column to store number of issues closed by a contributor
            
            df.loc[idx, "issues_closed"] = len(df_all_issues.loc[df_all_issues["issue_closed_by"]==contributor["login"]])
            
            # Need to get df for issue comments and PR comments
            df.loc[idx, "issue_pr_comments"] = len(df_all_comments.loc[df_all_comments["comment_by"] == contributor["login"]])
            
            # add a column to store number of commits made by a contributor
            df.loc[idx, "commits"] = len(git_obj.repos.get_commits(REPO_URL, contributor["login"]))
            idx +=1
        
        page += 1
    
    return df
```

### Get leaderboard


```python
def get_leaderboard(df):
    '''
    The function orders the given dataframe based on pts column in descending order.
    '''
    return df.sort_values(by="pts", ascending=False).reset_index(drop=True)

```

### Set Key Variables from function call


```python
df_all_issues = get_all_issues(REPO_URL)
print("Total open Issues fetched:", len(df_all_issues))
# df_all_issues.head()

df_all_comments = get_issue_pr_comments(REPO_URL)
# df_all_comments.head()

df_contributors = get_contributors_details(REPO_URL)
# df_contributors.head()
```

### Add pts column to contributor dataframe


```python
# Add a column of points for contributors df
# pts is calculated by multiplying a pre-defined wieght for each of the columns
# Feel free to modify the weight 
df_contributors["pts"] = 1*df_contributors["issues_created"] + 1*df_contributors["issues_closed"] + \
                        0.5*df_contributors["issue_pr_comments"] + 1*df_contributors["commits"]
```

## Output


```python
df_leaderboard = get_leaderboard(df_contributors)
print("Here are the top 10 contributors \n")
df_leaderboard.head(10)
```
