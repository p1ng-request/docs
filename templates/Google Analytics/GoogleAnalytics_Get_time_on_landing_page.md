<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Google Analytics - GoogleAnalytics Get time on landing page
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Analytics/GoogleAnalytics_Get_time_on_landing_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googleanalytics #timeonlanding

Pre-requisite: Create your own <a href="">Google API JSON credential</a>

## Input

### Import library


```python
from datetime import timedelta

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

### Time spent on landing page


```python
avg_time_on_landing = googleanalytics.views.get_time_landing(view_id=view_id, landing_path="/")
```

## Output

### Display result


```python
avg_time_on_landing['avg_time_landing']
```

# Plot Time spent on landing page


```python
def gen_tickvals(avg_time_landing: pd.Series) -> tuple:
    """
    Generate tick text and values.
    """
    delta = int(avg_time_landing.std() / 3)
    minimum = int(avg_time_landing.min() - delta)
    maximum = int(avg_time_landing.max() + delta)
    tickvals = list(range(minimum, maximum, delta))
    ticktext = [str(timedelta(seconds=v)) for v in tickvals]
    return tickvals, ticktext

def plot_time_spent_on_landing(df: pd.DataFrame):
    """
    Plot time spent on landing page in Plotly.
    """
    tickvals, ticktext = gen_tickvals(df['avg_time_landing'])
    data = go.Scatter(
        x=pd.to_datetime(df['Year Month'] + "01"),
        y=df['avg_time_landing']
    )

    fig = go.Figure(data=data)
    fig.update_traces(mode='lines+markers')
    fig.update_layout(title="Avg. Time on Landing Page (in seconds)", template="none")
    fig.update_yaxes(ticktext=ticktext, tickvals=tickvals)
    return fig
```


```python
plot_time_spent_on_landing(avg_time_on_landing)
```


```python
avg_time_on_landing['avg_time_landing']
```


```python
str(timedelta(seconds=70))
```


```python

```
