<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Horizontal_Barchart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Horizontal+Barchart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #chart #horizontalbar #dataviz #snippet #operations #image #html

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides instructions on how to create a horizontal bar chart using Plotly.

## Input

### Import library


```python
import plotly.graph_objects as go
```

## Model

### Create the plot


```python
fig = go.Figure(
    go.Bar(
        x=[20, 14, 23],
        y=["giraffes", "orangutans", "monkeys"],
        orientation="h",
        text=[20, 14, 23],
    )
)
fig.update_layout(
    title="Horizontal barchart",
    plot_bgcolor="#ffffff",
    width=1200,
    height=800,
    margin_pad=10,
    xaxis_showticklabels=False,
    bargap=0.1,  # gap between bars of adjacent location coordinates.
    bargroupgap=0.2,  # gap between bars of the same location coordinate.
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
