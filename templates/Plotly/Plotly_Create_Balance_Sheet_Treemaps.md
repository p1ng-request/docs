<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Balance_Sheet_Treemaps.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Balance+Sheet+Treemaps:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #treemap #snippet #dataviz #balancesheet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook displays Balance Sheet items into treemap graphs. In a balance sheet, treemap templates can be used to show the distribution of assets and liabilities. The assets can be divided into smaller categories such as cash, marketable securities, accounts receivable, and inventory, while the liabilities can be separated into categories like loans payable, bonds payable, and accounts payable. With a treemap, it is easy to see the relative proportions of each category, making it easier to identify any trends or patterns in the data.

<u>References</u>:
- https://plotly.com/python/treemaps/

## Input

### Import libraries


```python
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import pandas as pd
import naas
```

### Setup Variables


```python
# Inputs
# Create sample financial data
data_asset = {
    "ENTITY": ["Entity X"] * 5,
    "SCENARIO": ["2022-12"] * 5,
    "LABEL": [
        "Total Assets",
        "Accounts Receivable",
        "Inventory",
        "Property & Equipment",
        "Cash",
    ],
    "PARENT": ["", "Total Assets", "Total Assets", "Total Assets", "Total Assets"],
    "CATEGORY": ["Actif"] * 5,
    "VALUE": [35.4, 10.2, 2.5, 17.1, 5.6],
}

data_liability = {
    "ENTITY": ["Entity X"] * 5,
    "SCENARIO": ["2022-12"] * 5,
    "LABEL": [
        "Total Liabilities",
        "Equity",
        "Debt",
        "Accounts Payable",
        "Retained Earnings",
    ],
    "PARENT": [
        "",
        "Total Liabilities",
        "Total Liabilities",
        "Total Liabilities",
        "Total Liabilities",
    ],
    "CATEGORY": ["Actif"] * 5,
    "VALUE": [35.4, 16.8, 14.8, 1.2, 2.6],
}

# Outputs
html_output = "Plotly_BS_Treemap.html"
png_output = "Plotly_BS_Treemap.png"
```

## Model

### Get "Assets" data


```python
df_asset = pd.DataFrame(data_asset)
df_asset
```

### Get "Liabilities" data


```python
df_liability = pd.DataFrame(data_liability)
df_liability
```

### Create Treemap


```python
fig = make_subplots(
    cols=2,
    rows=1,
    horizontal_spacing=0.02,
    specs=[[{"type": "treemap", "rowspan": 1}, {"type": "treemap"}]],
)

fig.add_trace(
    go.Treemap(
        labels=df_asset["LABEL"],
        parents=df_asset["PARENT"],
        values=df_asset["VALUE"],
        textinfo="label+value+percent parent",
        marker_colorscale="Blues",
        hoverinfo="label+value+percent parent",
        branchvalues="total",
    ),
    row=1,
    col=1,
)

fig.add_trace(
    go.Treemap(
        labels=df_liability["LABEL"],
        parents=df_liability["PARENT"],
        values=df_liability["VALUE"],
        textinfo="label+value+percent parent",
        marker_colorscale="oranges",
        hoverinfo="label+value+percent parent",
        branchvalues="total",
    ),
    row=1,
    col=2,
)

fig.update_layout(
    title="Balance Sheet Breakdown", title_x=0.01, margin=dict(t=75, l=10, r=10, b=25)
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


```python

```


```python

```
