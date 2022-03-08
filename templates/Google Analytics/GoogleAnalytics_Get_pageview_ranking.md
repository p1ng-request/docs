<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Analytics/GoogleAnalytics_Get_pageview_ranking.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googleanalytics #pageviews

Pre-requisite: Create your own <a href="">Google API JSON credential</a>

## Input

### Import library


```python
import pandas as pd
import plotly.graph_objects as go

from naas_drivers import googleanalytics
```

### Get your credential from Google Cloud Platform


```python
json_path = '/Users/charlesdemontigny/Desktop/naas-335023-90c733ba64dd.json'
```

### Get view id from google analytics


```python
view_id = "236707574"
```

## Model

### Report Website - Google Analytics performance


```python
googleanalytics.connect(json_path=json_path)
```

### Ranking: Most visited web pages


```python
pageview = googleanalytics.views.get_pageview(view_id)
pageview.head()
```

## Output

### Display result


```python
pageview
```


```python
def plot_pageview(pageview: pd.DataFrame):
    """
    Plot PageView in Plotly.
    """
    data = go.Bar(y=pageview['Pages'],
                  x=pageview['Pageview'],
                  text=pageview['Pageview'],
                  orientation="h")
    layout = go.Layout(template="none", title="Most visited web pages, by total visits")
    fig = go.Figure(data=data, layout=layout)
    fig.update_layout(yaxis={'categoryorder':'total ascending'},
                      margin={"l":150, "pad": 20})
    fig.update_traces(textposition="outside")
    return fig
```


```python
plot_pageview(pageview)
```
