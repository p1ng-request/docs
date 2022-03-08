**Tags:** #plotly #chart #worldmap #dataviz

## Input

### Import libraries


```python
import naas
import plotly.graph_objects as go
import pandas as pd
```

### Variables


```python
title = "Worldmap"

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```

### Get data
Columns :
1. ISO code of country    
2. Value

To use the built-in countries geometry, provide locations as [three-letter ISO country codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3).


```python
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2014_world_gdp_with_codes.csv')
df
```

## Model

### Create the plot


```python
fig = go.Figure()

config = {'displayModeBar': False}

fig = go.Figure(data=go.Choropleth(
    locations = df['CODE'],
    z = df['GDP (BILLIONS)'],
    text = df['COUNTRY'],
    colorscale = 'Blues',
    autocolorscale=False,
    reversescale=True,
    marker_line_color='darkgray',
    marker_line_width=0.5,
    colorbar_tickprefix = '$',
    colorbar_title = 'GDP<br>Billions US$',
))

fig.update_layout(
    title=title ,
    plot_bgcolor="#ffffff",
    legend_x=1,
    geo=dict(
        showframe=False,
        showcoastlines=False,
        #projection_type='equirectangular'
    ),
    dragmode= False,
    #width=800,
    height=600,

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
