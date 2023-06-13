<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Treemaps_with_plotly.graph_objects.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Treemaps+with+plotly.graph+objects:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #treemap #snippet #dataviz #plotly.graph_objects #go

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates Treemaps with plotly.graph_objects.

<u>References:</u>
- https://plotly.com/python/treemaps/
- https://plotly.com/python/graph-objects/
- https://plotly.com/python/reference/treemap/

## Input

### Import libraries


```python
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import numpy as np
import pandas as pd
import naas
```

### Setup Variables


```python
# Outputs
html_output = "Treemap_plotly_graph_objects.html"
png_output = "Treemap_plotly_graph_objects.png"
```

## Model

### Basic Treemap with go.Treemap
If Plotly Express does not provide a good starting point, it is also possible to use the more generic go.Treemap class from plotly.graph_objects.


```python
fig = go.Figure(
    go.Treemap(
        labels=[
            "Eve",
            "Cain",
            "Seth",
            "Enos",
            "Noam",
            "Abel",
            "Awan",
            "Enoch",
            "Azura",
        ],
        parents=["", "Eve", "Eve", "Seth", "Seth", "Eve", "Eve", "Awan", "Eve"],
        root_color="lightgrey",
    )
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Set Different Attributes in Treemap
This example uses the following attributes:

1. values: sets the values associated with each of the sectors.
2. textinfo: determines which trace information appear on the graph that can be 'text', 'value', 'current path', 'percent root', 'percent entry', and 'percent parent', or any combination of them.
3. pathbar: a main extra feature of treemap to display the current path of the visible portion of the hierarchical map. It may also be useful for zooming out of the graph.
branchvalues: determines how the items in values are summed. When set to "total", items in values are taken to be value of all its descendants. In the example below Eva = 65, which is equal to 14 + 12 + 10 + 2 + 6 + 6 + 1 + 4. When set to "remainder", items in 
4. values corresponding to the root and the branches sectors are taken to be the extra part not part of the sum of the values at their leaves.


```python
labels = ["Eve", "Cain", "Seth", "Enos", "Noam", "Abel", "Awan", "Enoch", "Azura"]
parents = ["", "Eve", "Eve", "Seth", "Seth", "Eve", "Eve", "Awan", "Eve"]

fig = make_subplots(
    cols=2,
    rows=1,
    column_widths=[0.4, 0.4],
    subplot_titles=(
        "branchvalues: <b>remainder<br />&nbsp;<br />",
        "branchvalues: <b>total<br />&nbsp;<br />",
    ),
    specs=[[{"type": "treemap", "rowspan": 1}, {"type": "treemap"}]],
)

fig.add_trace(
    go.Treemap(
        labels=labels,
        parents=parents,
        values=[10, 14, 12, 10, 2, 6, 6, 1, 4],
        textinfo="label+value+percent parent+percent entry+percent root",
        root_color="lightgrey",
    ),
    row=1,
    col=1,
)

fig.add_trace(
    go.Treemap(
        branchvalues="total",
        labels=labels,
        parents=parents,
        values=[65, 14, 12, 10, 2, 6, 6, 1, 4],
        textinfo="label+value+percent parent+percent entry",
        root_color="lightgrey",
    ),
    row=1,
    col=2,
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Set Color of Treemap Sectors
There are three different ways to change the color of the sectors in Treemap:

marker.colors, 2) colorway, 3) colorscale. The following examples show how to use each of them.


```python
values = [0, 11, 12, 13, 14, 15, 20, 30]
labels = ["container", "A1", "A2", "A3", "A4", "A5", "B1", "B2"]
parents = ["", "container", "A1", "A2", "A3", "A4", "container", "B1"]

fig = go.Figure(
    go.Treemap(
        labels=labels,
        values=values,
        parents=parents,
        marker_colors=[
            "pink",
            "royalblue",
            "lightgray",
            "purple",
            "cyan",
            "lightgray",
            "lightblue",
            "lightgreen",
        ],
    )
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

This example uses treemapcolorway attribute, which should be set in layout.


```python
values = [0, 11, 12, 13, 14, 15, 20, 30]
labels = ["container", "A1", "A2", "A3", "A4", "A5", "B1", "B2"]
parents = ["", "container", "A1", "A2", "A3", "A4", "container", "B1"]

fig = go.Figure(
    go.Treemap(labels=labels, values=values, parents=parents, root_color="lightblue")
)

fig.update_layout(
    treemapcolorway=["pink", "lightgray"], margin=dict(t=50, l=25, r=25, b=25)
)
fig.show()
```


```python
values = [0, 11, 12, 13, 14, 15, 20, 30]
labels = ["container", "A1", "A2", "A3", "A4", "A5", "B1", "B2"]
parents = ["", "container", "A1", "A2", "A3", "A4", "container", "B1"]

fig = go.Figure(
    go.Treemap(labels=labels, values=values, parents=parents, marker_colorscale="Blues")
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))

fig.show()
```

### Treemap chart with a continuous colorscale
The example below visualizes a breakdown of sales (corresponding to sector width) and call success rate (corresponding to sector color) by region, county and salesperson level. For example, when exploring the data you can see that although the East region is behaving poorly, the Tyler county is still above average -- however, its performance is reduced by the poor success rate of salesperson GT.

In the right subplot which has a maxdepth of two levels, click on a sector to see its breakdown to lower levels.


```python
df = pd.read_csv(
    "https://raw.githubusercontent.com/plotly/datasets/master/sales_success.csv"
)
print(df.head())

levels = ["salesperson", "county", "region"]  # levels used for the hierarchical chart
color_columns = ["sales", "calls"]
value_column = "calls"


def build_hierarchical_dataframe(df, levels, value_column, color_columns=None):
    """
    Build a hierarchy of levels for Sunburst or Treemap charts.

    Levels are given starting from the bottom to the top of the hierarchy,
    ie the last level corresponds to the root.
    """
    df_all_trees = pd.DataFrame(columns=["id", "parent", "value", "color"])
    for i, level in enumerate(levels):
        df_tree = pd.DataFrame(columns=["id", "parent", "value", "color"])
        dfg = df.groupby(levels[i:]).sum()
        dfg = dfg.reset_index()
        df_tree["id"] = dfg[level].copy()
        if i < len(levels) - 1:
            df_tree["parent"] = dfg[levels[i + 1]].copy()
        else:
            df_tree["parent"] = "total"
        df_tree["value"] = dfg[value_column]
        df_tree["color"] = dfg[color_columns[0]] / dfg[color_columns[1]]
        df_all_trees = df_all_trees.append(df_tree, ignore_index=True)
    total = pd.Series(
        dict(
            id="total",
            parent="",
            value=df[value_column].sum(),
            color=df[color_columns[0]].sum() / df[color_columns[1]].sum(),
        )
    )
    df_all_trees = df_all_trees.append(total, ignore_index=True)
    return df_all_trees


df_all_trees = build_hierarchical_dataframe(df, levels, value_column, color_columns)
average_score = df["sales"].sum() / df["calls"].sum()

fig = make_subplots(
    1,
    2,
    specs=[[{"type": "domain"}, {"type": "domain"}]],
)

fig.add_trace(
    go.Treemap(
        labels=df_all_trees["id"],
        parents=df_all_trees["parent"],
        values=df_all_trees["value"],
        branchvalues="total",
        marker=dict(
            colors=df_all_trees["color"], colorscale="RdBu", cmid=average_score
        ),
        hovertemplate="<b>%{label} </b> <br> Sales: %{value}<br> Success rate: %{color:.2f}",
        name="",
    ),
    1,
    1,
)

fig.add_trace(
    go.Treemap(
        labels=df_all_trees["id"],
        parents=df_all_trees["parent"],
        values=df_all_trees["value"],
        branchvalues="total",
        marker=dict(
            colors=df_all_trees["color"], colorscale="RdBu", cmid=average_score
        ),
        hovertemplate="<b>%{label} </b> <br> Sales: %{value}<br> Success rate: %{color:.2f}",
        maxdepth=2,
    ),
    1,
    2,
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))
fig.show()
```

### Nested Layers in Treemap
The following example uses hierarchical data that includes layers and grouping. Treemap and Sunburst charts reveal insights into the data, and the format of your hierarchical data. maxdepth attribute sets the number of rendered sectors from the given level.


```python
df = pd.read_csv(
    "https://raw.githubusercontent.com/plotly/datasets/96c0bd/sunburst-coffee-flavors-complete.csv"
)

fig = go.Figure()

fig.add_trace(
    go.Treemap(
        ids=df.ids,
        labels=df.labels,
        parents=df.parents,
        maxdepth=3,
        root_color="lightgrey",
    )
)

fig.update_layout(margin=dict(t=50, l=25, r=25, b=25))

fig.show()
```

### Controlling text fontsize with uniformtext
If you want all the text labels to have the same size, you can use the uniformtext layout parameter. The minsize attribute sets the font size, and the mode attribute sets what happens for labels which cannot fit with the desired fontsize: either hide them or show them with overflow.

Note: animated transitions are currently not implemented when uniformtext is used.


```python
df = pd.read_csv(
    "https://raw.githubusercontent.com/plotly/datasets/96c0bd/sunburst-coffee-flavors-complete.csv"
)

fig = go.Figure(
    go.Treemap(
        ids=df.ids,
        labels=df.labels,
        parents=df.parents,
        pathbar_textfont_size=15,
        root_color="lightgrey",
    )
)
fig.update_layout(
    uniformtext=dict(minsize=10, mode="hide"), margin=dict(t=50, l=25, r=25, b=25)
)
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
