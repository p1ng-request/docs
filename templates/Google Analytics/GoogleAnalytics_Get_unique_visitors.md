<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Google Analytics - GoogleAnalytics Get unique visitors
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Analytics/GoogleAnalytics_Get_unique_visitors.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googleanalytics #getuniquevisitors

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

### Number of uniques visitors


```python
unique_visitors = googleanalytics.views.get_unique_visitors(view_id)
```

## Output

### Display result


```python
unique_visitors.tail()
```


```python
def plot_unique_visitors(unique_visitors: pd.DataFrame):
    """
    Plot PageView in Plotly.
    """
    data = go.Bar(x=pd.to_datetime(unique_visitors['Year Month'] + "01"),
                  y=unique_visitors['Users'],
                  text=unique_visitors['Users'],
                  orientation="v")
    layout = go.Layout(template="none", title="Number of Unique Visitors by Month")
    fig = go.Figure(data=data, layout=layout)
    fig.update_layout(yaxis={'categoryorder':'total ascending'},
                      margin={"l":150, "pad": 20})
    fig.update_traces(textposition="outside")
    return fig
```


```python
plot_unique_visitors(unique_visitors)
```


```python

```
