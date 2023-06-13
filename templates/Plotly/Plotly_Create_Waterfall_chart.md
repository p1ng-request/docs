<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Waterfall_chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Waterfall+chart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #chart #warterfall #dataviz #snippet #operations #image #html

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook provides instructions on how to create a Waterfall chart using Plotly.

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
fig = go.Figure(
    go.Waterfall(
        name="20",
        orientation="v",
        measure=["relative", "relative", "total", "relative", "relative", "total"],
        decreasing={"marker": {"color": "#d94228"}},
        increasing={"marker": {"color": "#5ee290"}},
        totals={"marker": {"color": "#3f3f3f"}},
        x=[
            "Sales",
            "Consulting",
            "Revenue",
            "Direct expenses",
            "Other expenses",
            "EBITDA",
        ],
        textposition="outside",
        text=["+60", "+80", "140", "-40", "-20", "80"],
        y=[60, 80, 0, -40, -20, 0],
        connector={"line": {"color": "white"}},
    )
)

fig.update_layout(
    title=title,
    plot_bgcolor="#ffffff",
    width=800,
    height=600,
    xaxis_tickfont_size=14,
    yaxis=dict(
        title="USD (millions)",
        titlefont_size=16,
        tickfont_size=14,
    ),
    legend=dict(x=0, y=1.0, bgcolor="white", bordercolor="white"),
    bargap=0.1,  # gap between bars of adjacent location coordinates.
    bargroupgap=0.1,  # gap between bars of the same location coordinate.
)
config = {"displayModeBar": False}
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
link_html = naas.asset.add(output_html, {"inline": True})

# -> Uncomment the line below to remove your assets
# naas.asset.delete(output_image)
# naas.asset.delete(output_html)
```


```python

```
