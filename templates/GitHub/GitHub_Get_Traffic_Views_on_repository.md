<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_Traffic_Views_on_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+Traffic+Views+on+repository:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #api #traffic #views #plotly #linechart #analytics

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get traffic views on a GitHub repository.

<u>References:</u>
- [GitHub API Documentation](https://developer.github.com/v3/)
- [GitHub Traffic API Documentation](https://developer.github.com/v3/repos/traffic/)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
import pandas as pd
import plotly.graph_objects as go
```

### Setup Variables
- Create your personal access token [here](https://github.com/settings/tokens)
- Select all scopes on "repo" section


```python
repo_url = "https://github.com/jupyter-naas/awesome-notebooks"
token = naas.secret.get("GITHUB_TOKEN") or "GITHUB_TOKEN"
```

## Model

### Get Traffic Views

This function will get the traffic views of a GitHub repository.


```python
def get_traffic_views(repo_url, token):
    # owner + name of the repository
    owner = repo_url.split("/")[-2]
    name = repo_url.split("/")[-1]
    url = f"https://api.github.com/repos/{owner}/{name}/traffic/views"
    headers = {"Authorization": f"token {token}"}
    response = requests.get(url, headers=headers)
    return response.json()


traffic_views = get_traffic_views(repo_url, token)
pprint(traffic_views)
```

## Output

### Display data


```python
print("-> Git views on the last 14 days")
print(f"Views count: {traffic_views.get('count')}")
print(f"Uniques viewer: {traffic_views.get('uniques')}")

df = pd.DataFrame(traffic_views.get("views"))
df
```

### Display graph


```python
fig = go.Figure()
fig.add_trace(
    go.Scatter(
        name="count",
        x=df["timestamp"],
        y=df["count"],
        mode="lines+markers",
        marker=dict(color="blue"),
    )
)
fig.add_trace(
    go.Scatter(
        name="uniques",
        x=df["timestamp"],
        y=df["uniques"],
        mode="lines+markers",
        marker=dict(color="orange"),
    )
)
fig.update_layout(title="Git Views")
fig.show()
```


```python

```
