<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Plotly - Waterfall chart simple
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Waterfall_chart_simple.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #warterfall #dataviz

## Input

### Import libraries


```python
import naas
import plotly.graph_objects as go
```

### Variables


```python
title = "EBITDA (simple)"

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```

## Model

### Create Waterfall chart


```python
fig = go.Figure(go.Waterfall(
    name = "20", orientation = "v",
    measure = ["relative", "relative", "total", "relative", "relative", "total"],
    decreasing = {"marker":{"color":"#d94228"}},
    increasing = {"marker":{"color":"#5ee290"}},
    totals = {"marker":{"color":"#3f3f3f"}},
    x = ["Sales", "Consulting", "Revenue", "Direct expenses", "Other expenses", "EBITDA"],
    textposition = "outside",
    text = ["+60", "+80", "140", "-40", "-20", "80"],
    y = [60, 80, 0, -40, -20, 0],
    connector = {"line":{"color":"white"}},
))

fig.update_layout(
    title=title ,
    plot_bgcolor="#ffffff",
    #width=800,
    height=500,
    xaxis_tickfont_size=14,
    yaxis=dict(
        title='USD (millions)',
        titlefont_size=16,
        tickfont_size=14,
    ),
    legend=dict(
        x=0,
        y=1.0,
        bgcolor='white',
        bordercolor='white'
    ),
    bargap=0.1, # gap between bars of adjacent location coordinates.
    bargroupgap=0.1 # gap between bars of the same location coordinate.
)
fig.show()
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
