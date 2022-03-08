<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_stargazers_from_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook enables you to get a dataframe of all the stargazers of a particular Github repository.

**Tags:** #github #stars #naas_drivers

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

## Input

### Imports


```python
import pandas as pd
import requests
import os
from urllib.parse import urlencode
from datetime import datetime
import plotly.graph_objects as go
from naas_drivers import github
```

### Variables


```python
REPO_URL = "https://github.com/jupyter-naas/awesome-notebooks"
GITHUB_TOKEN = "ghp_COJiJEU4cxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

## Model

### Get stargazers


```python
df_stargazers = github.connect(GITHUB_TOKEN).repos.get_stargazers(REPO_URL)
df_stargazers
```

## Output

### Plotting a line chart to get trend


```python
def get_trend(df,
              date_col_name='STARRED_AT',
              value_col_name="ID",
              date_order='asc'):
    
    # Format date
    df[date_col_name] = pd.to_datetime(df[date_col_name]).dt.strftime("%Y-%m-%d")
    df = df.groupby(date_col_name, as_index=False).agg({value_col_name: "count"})
    d = datetime.now().date()
    d2 = df.loc[df.index[0], date_col_name]
    idx = pd.date_range(d2, d, freq = "D")
    
    df.set_index(date_col_name, drop=True, inplace=True)
    df.index = pd.DatetimeIndex(df.index)
    df = df.reindex(idx, fill_value=0)
    df[date_col_name] = pd.DatetimeIndex(df.index)
    
    # Calc sum cum
    df["value_cum"] = df.agg({value_col_name: "cumsum"})
    return df.reset_index(drop=True)

df_trend = get_trend(df_stargazers)
df_trend.tail(1)
```


```python
def create_linechart(df, date, value, repo_url):
    # Get repo name
    repo_name = repo_url.split("https://github.com/")[-1].split("/")[-1]
    
    # Get last value
    last_value = df.loc[df.index[-1], value]
    
    # Init
    fig = go.Figure()
    
    # Create fig
    fig.add_trace(
        go.Scatter(
            x=df[date].to_list(),
            y=df[value].to_list(),
            mode="lines+text",
            line=dict(color="black"),
        )
    )
    fig.update_traces(marker_color='black')
    fig.update_layout(
        title=f"⭐<b> Stars - {repo_name}</b><br><span style='font-size: 13px;'>Total stars as of today: {last_value}</span>",
        title_font=dict(family="Arial", size=18, color="black"),
        plot_bgcolor="#ffffff",
        width=1200,
        height=800,
        paper_bgcolor="white",
        xaxis_title="Date",
        xaxis_title_font=dict(family="Arial", size=11, color="black"),
        yaxis_title='No. of stars',
        yaxis_title_font=dict(family="Arial", size=11, color="black"),
        margin_pad=10,
    )
    fig.show()
    return fig

fig = create_linechart(df_trend, "STARRED_AT", "value_cum", REPO_URL)
```
