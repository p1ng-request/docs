<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FEC/FEC_Visualiser_Bilan_Treemap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FEC+-+Visualiser+Bilan+Treemap:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fec #plotly #treemap #snippet #dataviz

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** Ce notebook affiche les éléments du bilan sous forme de graphique treemap. Le graphique "treemap" est très utile pour montrer la répartition des actifs et des passifs.

<u>References:</u>
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
    "ENTITY": ["Société X"] * 5,
    "SCENARIO": ["2022-12"] * 5,
    "LABEL": [
        "Total Actif",
        "Créances clients",
        "Stocks",
        "Immobilisations",
        "Trésorerie",
    ],
    "PARENT": ["", "Total Actif", "Total Actif", "Total Actif", "Total Actif"],
    "CATEGORY": ["Actif"] * 5,
    "VALUE": [35.4, 10.2, 2.5, 17.1, 5.6],
}

data_liability = {
    "ENTITY": ["Société X"] * 5,
    "SCENARIO": ["2022-12"] * 5,
    "LABEL": ["Total Passif", "Capitaux propres", "Dettes", "Emprunts", "Provisions"],
    "PARENT": ["", "Total Passif", "Total Passif", "Total Passif", "Total Passif"],
    "CATEGORY": ["Actif"] * 5,
    "VALUE": [35.4, 16.8, 14.8, 1.2, 2.6],
}

# Outputs
html_output = "Bilan_Treemap.html"
png_output = "Bilan_Treemap.png"
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
    title="Décomposition du Bilan", title_x=0.01, margin=dict(t=50, l=10, r=10, b=25)
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
