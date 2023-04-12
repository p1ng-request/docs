<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WorldBank/WorldBank_Gini_index.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WorldBank+-+Gini+index:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #worldbank #opendata #snippet #plotly

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook provides an analysis of the Gini index, a measure of income inequality, from the World Bank.

## Input

### Import library


```python
import pandas as pd
from pandas_datareader import wb
import plotly.graph_objects as go
import plotly.express as px
```

## Model

### Get the association between the country and the ISO code


```python
countries = wb.get_countries()
countries = countries[["name", "iso3c"]]
countries.columns = ["country", "iso3c"]
countries
```

### Get gini index indicator per country


```python
indicators = wb.download(indicator=["SI.POV.GINI"], country="all", start=1967, end=2018)
indicators.columns = ["GINI_INDEX"]
indicators
```

### Merge previous tables


```python
master_table = pd.merge(
    indicators.reset_index(), countries, left_on="country", right_on="country"
)
master_table = master_table.set_index(["country", "iso3c", "year"])
master_table
```

### Pivot previous table and fill in undefined values with values from previous years


```python
pivoted_table = pd.pivot_table(
    master_table, index=["country", "iso3c"], columns="year", values="GINI_INDEX"
)
pivoted_table = pivoted_table.ffill(axis=1)
pivoted_table
```

### Show a map of gini index per country over the years (from 1969 to 2018)


```python
pivoted_table = pd.pivot_table(
    master_table, index=["country", "iso3c"], columns="year", values="GINI_INDEX"
)
pivoted_table = pivoted_table.ffill(axis=1)
countries = list(pivoted_table.index.get_level_values(0))
locations = list(pivoted_table.index.get_level_values(1))

data = []
steps = []
i = 0
for year in pivoted_table.columns:
    data.append(
        dict(
            type="choropleth",
            name="",
            locations=locations,
            z=pivoted_table[year],
            hovertext=countries,
            colorscale=px.colors.sequential.Reds,
            visible=year == "2018",
        )
    )

    step = dict(
        method="restyle",
        args=["visible", [False] * len(pivoted_table.columns)],
        label=year,
    )
    step["args"][1][i] = True
    steps.append(step)

    i = i + 1

layout = go.Layout(
    title=dict(
        text="Evolution of the gini index from 1969 to 2018",
        x=0.5,
        font=dict(
            size=21,
        ),
    ),
    sliders=[dict(steps=steps, active=len(data) - 1)],
    annotations=[
        dict(text="Updated in 2018 from The World Bank", showarrow=False, x=1, y=-0.05)
    ],
    autosize=True,
    height=800,
)

fig = go.Figure(data, layout)
fig
```

## Output

### Export HTML


```python
fig.write_html("file.html")
```
