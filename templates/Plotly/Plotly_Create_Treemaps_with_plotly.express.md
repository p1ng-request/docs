<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Treemaps_with_plotly.express.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Treemaps+with+plotly.express:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #treemap #snippet #dataviz #plotly.express #px

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates Treemaps with plotly.express. Plotly Express is the easy-to-use, high-level interface to Plotly, which operates on a variety of types of data and produces easy-to-style figures.

<u>References:</u>
- https://plotly.com/python/treemaps/
- https://plotly.com/python-api-reference/generated/plotly.express.treemap

## Input

### Import libraries


```python
import plotly.express as px
import numpy as np
import pandas as pd
import naas
```

### Setup Variables


```python
# Outputs
html_output = "Treemap_plotly_express.html"
png_output = "Treemap_plotly_express.png"
```

## Model

### Basic Treemap with plotly.express
With px.treemap, each row of the DataFrame is represented as a sector of the treemap.


```python
fig = px.treemap(
    names=["Eve", "Cain", "Seth", "Enos", "Noam", "Abel", "Awan", "Enoch", "Azura"],
    parents=["", "Eve", "Eve", "Seth", "Seth", "Eve", "Eve", "Awan", "Eve"],
)
fig.update_traces(root_color="lightgrey")
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Treemap of a rectangular DataFrame with plotly.express
Hierarchical data are often stored as a rectangular dataframe, with different columns corresponding to different levels of the hierarchy. px.treemap can take a path parameter corresponding to a list of columns. Note that id and parent should not be provided if path is given.


```python
df = px.data.tips()
fig = px.treemap(
    df, path=[px.Constant("all"), "day", "time", "sex"], values="total_bill"
)
fig.update_traces(root_color="lightgrey")
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Treemap of a rectangular DataFrame with continuous color argument in px.treemap
If a color argument is passed, the color of a node is computed as the average of the color values of its children, weighted by their values.

Note: for best results, ensure that the first path element is a single root node. In the examples below we are creating a dummy column containing identical values for each row to achieve this.


```python
df = px.data.gapminder().query("year == 2007")
fig = px.treemap(
    df,
    path=[px.Constant("world"), "continent", "country"],
    values="pop",
    color="lifeExp",
    hover_data=["iso_alpha"],
    color_continuous_scale="RdBu",
    color_continuous_midpoint=np.average(df["lifeExp"], weights=df["pop"]),
)
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Treemap of a rectangular DataFrame with discrete color argument in px.treemap
When the argument of color corresponds to non-numerical data, discrete colors are used. If a sector has the same value of the color column for all its children, then the corresponding color is used, otherwise the first color of the discrete color sequence is used.


```python
df = px.data.tips()
fig = px.treemap(
    df,
    path=[px.Constant("all"), "sex", "day", "time"],
    values="total_bill",
    color="day",
)
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

In the example below the color of Saturday and Sunday sectors is the same as Dinner because there are only Dinner entries for Saturday and Sunday. However, for Female -> Friday there are both lunches and dinners, hence the "mixed" color (blue here) is used.


```python
df = px.data.tips()
fig = px.treemap(
    df,
    path=[px.Constant("all"), "sex", "day", "time"],
    values="total_bill",
    color="time",
)
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Using an explicit mapping for discrete colors
For more information about discrete colors, see the [dedicated page](https://plotly.com/python/discrete-color/).


```python
df = px.data.tips()
fig = px.treemap(
    df,
    path=[px.Constant("all"), "sex", "day", "time"],
    values="total_bill",
    color="time",
    color_discrete_map={"(?)": "lightgrey", "Lunch": "gold", "Dinner": "darkblue"},
)
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Rectangular data with missing values
If the dataset is not fully rectangular, missing values should be supplied as None.


```python
vendors = ["A", "B", "C", "D", None, "E", "F", "G", "H", None]
sectors = [
    "Tech",
    "Tech",
    "Finance",
    "Finance",
    "Other",
    "Tech",
    "Tech",
    "Finance",
    "Finance",
    "Other",
]
regions = [
    "North",
    "North",
    "North",
    "North",
    "North",
    "South",
    "South",
    "South",
    "South",
    "South",
]
sales = [1, 3, 2, 4, 1, 2, 2, 1, 4, 1]
df = pd.DataFrame(dict(vendors=vendors, sectors=sectors, regions=regions, sales=sales))
df["all"] = "all"  # in order to have a single root node
print(df)
fig = px.treemap(df, path=["all", "regions", "sectors", "vendors"], values="sales")
fig.update_traces(root_color="lightgrey")
fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

## Output

### Save and share your graph as PNG


```python
fig.write_image(png_output)

# Share output with naas
naas.asset.add(png_output)

# -> Uncomment the line below to remove your asset
# naas.asset.delete(html_output)
```

### Save and share your graph as HTML


```python
fig.write_html(html_output)

# Share output with naas
naas.asset.add(html_output, params={"inline": True})

# -> Uncomment the line below to remove your asset
# naas.asset.delete(html_output)
```
