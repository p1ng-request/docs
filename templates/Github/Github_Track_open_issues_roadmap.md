<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Track_open_issues_roadmap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

The objective of the notebook is to maintain a track of issues that are open in the community roadmap

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
PROJECT_URL = "https://github.com/orgs/jupyter-naas/projects"
GITHUB_TOKEN = "ghp_COJiJEU4cQR4rjslUjM9Dupxxxxxxxxxxxxxxxxxxx"
```

## Model

### Get projects active on Github


```python
def get_active_project_links(token, url):
    project_df = pd.DataFrame()
    headers={"Authorization":f'token {token}'}
    url = "api.github.com".join(url.split("github.com"))
    page=1
    while True:
        params = {
            "per_page":100,
            'page':page
        }
        url_link = url+ f"?{urlencode(params, safe='(),')}"
        res = requests.get(url_link, headers=headers)
        
        try:
            res.raise_for_status()
        except requests.HTTPError as e:
            raise(e)
        if len(res.json())==0:
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
df_projects.head()
```

### Get comments from issues


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

### Get details regarding issues from projects


```python
def get_issues_from_projects(token, project_url):
    df_projects = get_active_project_links(token, project_url)
    df_issues = pd.DataFrame(columns=['issue_status', 'issue_state'])
    headers={"Authorization":f'token {token}'}
    
    ## Gets info from columns present in our roadmap ##
    for _, project in df_projects.iterrows():
        
        columns = requests.get(project['project_columns_url'], headers=headers).json()
        issue_status, issue_urls=[],[]
        for column in columns:
            page=1
            while True:
                params = {
                    'per_page':100,
                    'page':page
                }
                card_url = column['cards_url']+ f"?{urlencode(params, safe='(),')}"
                issues = requests.get(card_url, headers=headers)
                try:
                    issues.raise_for_status()
                except requests.HTTPError as e:
                    raise(e)
                if len(issues.json()) == 0:
                    break
                for issue in issues.json():
                    if issue.get('content_url')!=None:                        
                        issue_urls.append(issue.get('content_url'))
                        issue_status.append(column['name'])
                page+=1
                
        df_issues['issue_status'] = issue_status
        
        for idx, url in enumerate(issue_urls):
            issue = requests.get(url, headers=headers)
            try:
                issue.raise_for_status()
            except requests.HTTPError as e:
                raise(e)
            issue = issue.json()
            ###### information to be extracted are below #####
            df_issues.loc[idx, 'link_to_the_issue'], df_issues.loc[idx, 'issue_number'] = issue['html_url'], issue['number']
            df_issues.loc[idx, 'issue_title'], df_issues.loc[idx, 'issue_state'] = issue['title'], issue['state']

            labels= []
            for label in issue['labels']:
                labels.append(label.get('name'))
            df_issues.loc[idx, 'issue_labels'] = ", ".join(labels)

            assigned=[]
            for assignee in issue['assignees']:
                assigned.append(assignee.get('login'))
            if assigned==[]:
                df_issues.loc[idx, 'issue_assignees'] = 'None'
            else:
                df_issues.loc[idx, 'issue_assignees'] = ", ".join(assigned)

            df_issues.loc[idx, 'comments_till_date'] = issue['comments']

            df_issues.loc[idx, 'last_created_date'] = issue.get('created_at').strip('Z').split('T')[0]
            df_issues.loc[idx, 'last_created_time'] = issue.get('created_at').strip('Z').split('T')[-1]
            df_issues.loc[idx, 'last_updated_date'] = issue.get('updated_at').strip('Z').split('T')[0]
            df_issues.loc[idx, 'last_updated_time'] = issue.get('updated_at').strip('Z').split('T')[-1]

            if df_issues.loc[idx, 'issue_status']!='Backlog':
                date_format = "%Y-%m-%d"
                delta = datetime.now() - datetime.strptime(df_issues.loc[idx, 'last_updated_date'], date_format)
                df_issues.loc[idx, 'stale_issue'] = f'No activity since {delta.days} days'
            else:
                df_issues.loc[idx, 'stale_issue'] = 'None'
            
            df_issues.loc[idx, 'comments'] = str(get_comments_from_issues(token, issue['comments_url']))
            
            try:
                pr = requests.get(issue.get('pull_request')['url'], headers= headers).json()
                df_issues.loc[idx, 'linked_pr_state'] = pr.get('state')
                
                date_format = "%Y-%m-%d"
                delta = datetime.now() - datetime.strptime(pr.get('updated_at').split('T')[0], date_format)
                df_issues.loc[idx, 'PR_activity'] = f'No activity since {delta.days} days'
                
            except:
                df_issues.loc[idx, 'linked_pr_state'] = 'None'
                df_issues.loc[idx, 'PR_activity'] = 'None'
            ##################################################
        
        df_issues['project_id'] = [df_projects.project_id.values[0]]*df_issues.shape[0]
        df_issues['project_name'] = [df_projects.project_name.values[0]]*df_issues.shape[0]
        df_issues['issue_number'] = df_issues['issue_number'].apply(lambda x: int(x))
        df_issues['comments_till_date'] = df_issues['comments_till_date'].apply(lambda x: int(x))
        
    return df_issues

df_issues = get_issues_from_projects(GITHUB_TOKEN, PROJECT_URL)
```


```python
df_issues.tail(15)
```

## Output

### Save data in csv


```python
df_issues.to_csv("GITHUB_Issues.csv", index=False)
```

### Plotting a bar graph for total number of issues


```python
def create_barchart(df, title, labels):
    status = df.issue_status.unique()
    x_list = []
    x_order = ["Backlog", "To do", "In progress", "Review", "Done"]
    for x in x_order:
        if x in status:
            x_list += [x]
    
    # Create fig
    fig = px.bar(df,
           title= title,
           x=x_list,
           y="count",
           text="count",
           labels=labels)
    fig.update_traces(marker_color='black')
    fig.update_layout(
        plot_bgcolor="#ffffff",
        width=1000,
        height=800,
        font=dict(family="Arial", size=14, color="black"),
        paper_bgcolor="white",
        yaxis_title="No of issues",
        yaxis_title_font=dict(family="Arial", size=11, color="black"),
        xaxis_title="Status",
        xaxis_title_font=dict(family="Arial", size=11, color="black"),
        margin_pad=10,
    )
    fig.show()
    return fig
```


```python
issues = df_issues.groupby('issue_status').agg(
    {'issue_number':'count'}).reset_index().rename(
    columns={"issue_number":"count"})

title =  f"Github Project - {PROJECT_URL.split('/')[-2]} : {df_issues['project_name'].unique()[0]} <br><span style='font-size: 13px;'>Total issues: {issues['count'].sum()}</span>"
labels = {
               'issue_status':'Issue status',
               'count':"Number of Issues"
          }
fig = create_barchart(issues, title, labels)
```

### Plotting a bar graph for open issues


```python
open_issues = df_issues[df_issues['issue_state']=='open'].groupby('issue_status').agg({"issue_number":'count'}).reset_index().rename(columns={'issue_number':'count'})

title =  f"Github Project - {PROJECT_URL.split('/')[-2]} : {df_issues['project_name'].unique()[0]} <br><span style='font-size: 13px;'>Total open issues: {open_issues['count'].sum()}</span>"
labels = {
               'issue_status':'Issue status',
               'count':"Number of Open issues"
          }
fig = create_barchart(open_issues, title, labels)
```

### Plotting a bar graph for closed issues


```python
closed_issues = df_issues[df_issues['issue_state']=='closed'].groupby('issue_status').agg({"issue_number":'count'}).reset_index().rename(columns={'issue_number':'count'})

title =  f"Github Project - {PROJECT_URL.split('/')[-2]} : {df_issues['project_name'].unique()[0]} <br><span style='font-size: 13px;'>Total closed issues: {closed_issues['count'].sum()}</span>"
labels = {
               'issue_status':'Issue status',
               'count':"Number of Closed issues"
          }

fig = create_barchart(closed_issues, title, labels)
```

### Plotting a bar graph for stale issues


```python
stale_issues=[]
for item in df_issues.stale_issue:
    if item!='None':
        stale_issues.append(int(item.split()[-2])>=7)
    else:
         stale_issues.append(False)
```


```python
df_issues['stale_bool'] = stale_issues
temp = df_issues[df_issues['stale_bool']==True]
temp[temp['issue_state']=='open']

open_stale_issues = temp[temp['issue_state']=='open'].groupby('issue_status').agg({"stale_bool":'count'}).reset_index().rename(columns={'stale_bool':'count'})

title =  f"Github Project - {PROJECT_URL.split('/')[-2]} : {df_issues['project_name'].unique()[0]} <br><span style='font-size: 13px;'>Total open stale issues: {open_stale_issues['count'].sum()}</span>"
labels = {
               'issue_status':'Issue status',
               'count':"Number of Open issues with no activity since more than 7 days"
          }
fig = create_barchart(open_stale_issues, title, labels)
```


```python

```
