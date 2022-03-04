<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Github - Track notebooks created over time
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Track_notebooks_created_over_time.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #github #repos #commits #notebooks

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input


```python
import pandas as pd
import requests
import os
from naas_drivers import plotly, github
import pydash as _pd
from urllib.parse import urlencode
from datetime import datetime, timedelta
```

## Setup Github
**How to find your personal access token on Github?**

- First we need to create a personal access token to get the details of our organization from here: https://github.com/settings/tokens
- You will be asked to select scopes for the token. Which scopes you choose will determine what information and actions you will be able to perform against the API.
- You should be careful with the ones prefixed with write:, delete: and admin: as these might be quite destructive.
- You can find description of each scope in docs here (https://docs.github.com/en/developers/apps/building-oauth-apps/scopes-for-oauth-apps).


```python
GITHUB_TOKEN = "ghp_Stz3qlkR3b00nKUW8rxJobxxxxxxxxxx"
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"
```

### Get commits


```python
df_commits = github.connect(GITHUB_TOKEN).repositories.get_commits(REPO_URL)
print("Total commits:", len(df_commits))
df_commits.head(1)
```

## Model

### Filter on merge PR and date


```python
def get_commits_merge(df):
    df_pr = df[(df.MESSAGE.str[:5] == "Merge") & 
               (df.VERIFICATION_STATUS == True)].reset_index(drop=True)
    print("Total Merged PR:", len(df_pr))

    df_pr["DATE"] = df_pr["AUTHOR_DATE"].dt.strftime("%Y-%m-%d")
    df_pr = df_pr[["DATE", "COMMITTER_NAME", "ID"]].drop_duplicates("DATE").reset_index(drop=True)
    print("Total Merged PR (unique date):", len(df_pr))
    return df_pr

df_pr = get_commits_merge(df_commits)
df_pr.head(1)
```

### Get notebooks for each commits


```python
def get_notebooks(commit_id):
    commits = []
    headers = {'Authorization': f'token {GITHUB_TOKEN}'}
    url = f"https://api.github.com/repos/jupyter-naas/awesome-notebooks/git/trees/{commit_id}"
    res = requests.get(url, headers=headers)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        raise(e)
    res_json = res.json()

    trees = res_json.get("tree")
    for t in trees:
        path = t.get("path")
        if not "." in path and path != "LICENSE":
            url = t.get("url")
            res = requests.get(url, headers=headers)
            try:
                res.raise_for_status()
            except requests.HTTPError as e:
                raise(e)
            res_tree = res.json()
            sub_trees = res_tree.get("tree")
            if sub_trees is not None:
                for s in sub_trees:
                    sub_path = s.get("path")
                    if sub_path.endswith(".ipynb"):
                        commit = {
                            "FOLDER": path,
                            "NOTEBOOK" : sub_path
                        }
                        commits.append(commit)
                    elif not "." in sub_path:
                        sub_url = s.get("url")
                        res = requests.get(sub_url, headers=headers)
                        try:
                            res.raise_for_status()
                        except requests.HTTPError as e:
                            raise(e)
                        res_tree = res.json()
                        sub_trees = res_tree.get("tree")
                        if sub_trees is not None:
                            for s in sub_trees:
                                sub_path = s.get("path")
                                if sub_path.endswith(".ipynb"):
                                    commit = {
                                        "FOLDER": path,
                                        "NOTEBOOK" : sub_path
                                    }
                                    commits.append(commit)
    return pd.DataFrame(commits)
```


```python
def get_notebooks(commit_id):
    notebooks = []
    headers = {'Authorization': f'token {GITHUB_TOKEN}'}
    url = f"https://api.github.com/repos/jupyter-naas/awesome-notebooks/git/trees/{commit_id}?recursive=1"
    res = requests.get(url, headers=headers)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        raise(e)
    res_json = res.json()

    trees = res_json.get("tree")
    for file in trees:
        if ".github" not in file.get("path") and ".gitignore" not in file.get("path") and "/" in file.get("path"):
            if file.get("path").endswith(".ipynb"):
                temp = file.get("path").split("/")
                if temp == -1:
                    data = {
                        "root": None,
                        "subdir": file.get("path")
                    }
                    notebooks.append(data)
                else:
                    last_folder = ""
                    file_name = temp[-1]
                    temp.pop()
                    for folder in temp:
                        last_folder += "/" + folder
                    root = last_folder[1:]
                    data = {
                        "root": root,
                        "subdir": file_name
                    }
                    notebooks.append(data)
    return pd.DataFrame(notebooks)
```


```python
df_tracks = pd.DataFrame()

for _, row in df_pr.iterrows():
    date = row.DATE
    commit_id = row.ID
    try:
        df_track = get_notebooks(commit_id)
        df_track["DATE"] = date
        df_track["ID"] = commit_id
        # Concat
        df_tracks = pd.concat([df_tracks, df_track], axis=0)
    except Exception as e:
        print(f"Error on {date} - {commit_id}", e)

print("Total notebooks tracked:", len(df_tracks))       
df_tracks.head(1)
```

## Output

### Save notebooks tracks in CSV


```python
df_tracks.to_csv("TRACKS.csv", index=False)
```

### Plotting a line chart for notebook commits


```python
def get_trend(df,
              date_col_name='DATE',
              date_order='asc'):
    
    df = df.groupby(date_col_name, as_index=False).agg({"ID": "count"})
    d = datetime.now().date()
    d2 = df.loc[df.index[0], date_col_name]
    idx = pd.date_range(d2, d, freq = "D")
    
    df.set_index(date_col_name, drop=True, inplace=True)
    df.index = pd.DatetimeIndex(df.index)
    df = df.reindex(idx, fill_value=0)
    df[date_col_name] = pd.DatetimeIndex(df.index)
    df = df.reset_index(drop=True)
    for _, row in df.iterrows():
        if _ > 0:
            n_1 = df.loc[df.index[_-1], "ID"]
            n = df.loc[df.index[_], "ID"]
            if n == 0:
                df.loc[_, "ID"] = n_1
        
    return df

df_notebooks = get_trend(df_tracks)
df_notebooks
```


```python
import plotly.graph_objects as go

def create_linechart(df):
    # Calc commits
    notebooks = df.loc[df.index[-1], "ID"]
    
    # Init
    fig = go.Figure()
    
    # Create fig
    fig.add_trace(
        go.Scatter(
            x=df.DATE.to_list(),
            y=df.ID.to_list(),
            mode="lines+text",
            line=dict(color="black"),
        )
    )
    fig.update_traces(marker_color='black')
    fig.update_layout(
        title=f"<b>Tracks of notebooks created since naas launch </b><br><span style='font-size: 13px;'>Total notebooks as of today: {notebooks}</span>",
        title_font=dict(family="Arial", size=18, color="black"),
        plot_bgcolor="#ffffff",
        width=1200,
        height=800,
        paper_bgcolor="white",
        xaxis_title='Date',
        xaxis_title_font=dict(family="Arial", size=11, color="black"),
        yaxis_title='Nb. of notebooks',
        yaxis_title_font=dict(family="Arial", size=11, color="black"),
        margin_pad=10,
    )
    fig.show()
    return fig

fig = create_linechart(df_notebooks)
```
