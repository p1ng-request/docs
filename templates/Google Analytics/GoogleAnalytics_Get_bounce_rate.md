<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Google Analytics - GoogleAnalytics Get bounce rate
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Analytics/GoogleAnalytics_Get_bounce_rate.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googleanalytics #bouncerate

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

### Bounce Rate


```python
bounce_rate = googleanalytics.views.get_bounce_rate(view_id=view_id)
```

## Output

### Display result


```python
bounce_rate
```

# Bounce Rate Plot


```python
def plot_bounce_rate(bounce_rate: pd.DataFrame):
    """
    Plot bounce rate as an area chart in Plotly.
    """
    data = go.Scatter(
        x=pd.to_datetime(bounce_rate['Year Month'] + "01"),
        y=bounce_rate['Bounce Rate'],
        stackgroup="one"
    )

    fig = go.Figure(data=data)
    fig.update_traces(mode='lines+markers')
    fig.update_layout(yaxis={"tickformat": ',.0%'}, title="Bounce Rate", template="none")
    return fig
```


```python
plot_bounce_rate(bounce_rate)
```


```python

```
