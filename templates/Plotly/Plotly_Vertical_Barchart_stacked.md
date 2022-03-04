# Plotly - Vertical Barchart stacked
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Vertical_Barchart_stacked.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #verticalbarchart #group #dataviz

## Input

### Import libraries


```python
import naas
import plotly.graph_objects as go
```

### Variables


```python
title = "Sales Evolution (group)"

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```

### Get data


```python
x_axis = [1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012]

y_axis_value1 = [219, 146, 112, 127, 124, 180, 236, 207, 236, 263, 350, 430, 474, 526, 488, 537, 500, 439]

y_axis_value2 = [16, 13, 10, 11, 28, 37, 43, 55, 56, 88, 105, 156, 270, 299, 340, 403, 549, 499]
```

## Model

### Create Vertical Barchart stacked


```python
fig = go.Figure()

Value1 = "USA"
Value2 = "Rest of world"

fig.add_trace(go.Bar(x=x_axis,
                y= y_axis_value1,
                name= Value1,
                marker_color='#5ee290'
                ))
fig.add_trace(go.Bar(x=x_axis,
                y= y_axis_value2,
                name= Value2,
                marker_color='#3f3f3f'
                ))

#fig.update_layout( hovermode="x", title=title)

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
    barmode='stack',
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
