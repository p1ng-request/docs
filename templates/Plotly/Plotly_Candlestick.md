# Plotly - Candlestick
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Candlestick.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #candlestick #group #dataviz

## Input

### Import libraries


```python
import naas
from naas_drivers import yahoofinance
import plotly.graph_objects as go
import pandas as pd
```

### Variables


```python
title = "Candlestick"

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```

### Get data


```python
date_from = -360 # Date can be number or date or today
date_to = "today"
df = yahoofinance.get("TSLA", date_from=date_from, date_to=date_to)
df
```

## Model

### Create Candlestick


```python
fig = go.Figure()

config = {'displayModeBar': False}

fig = go.Figure(data=[go.Candlestick(x=df['Date'],
                open=df['Open'],
                high=df['High'],
                low=df['Low'],
                close=df['Close'])])

fig.update_layout(
    title=title,
    plot_bgcolor="#ffffff",
    #width=800,
    height=600,
    xaxis_tickfont_size=14,
    yaxis=dict(
        title='Price in $',
        titlefont_size=16,
        tickfont_size=14,
    )
)
fig.show(config=config)
```

## Output

### Export in PNG and HTML


```python
fig.write_image(output_image, width=1200)
fig.write_html(output_html)
```

### Generate shareable assets


```python
link_image = naas.asset.add(output_image)
link_html = naas.asset.add(output_html, {"inline":True})
```


```python

```
