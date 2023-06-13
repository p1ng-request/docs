<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FEC/FEC_Visualiser_Charges_Horizontal_Barchart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FEC+-+Visualiser+Charges+Horizontal+Barchart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fec #plotly #horizontalbarchart #visualisation #charges #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** Ce notebook vous permettra de visualiser les charges de votre entreprise à l'aide d'un barchart horizontal.

**References:**
- [Plotly Documentation](https://plotly.com/python/reference/)
- [Plotly Horizontal Barchart](https://plotly.com/python/horizontal-bar-charts/)

## Input

### Import libraries


```python
import plotly.graph_objects as go
import pandas as pd
import naas
```

### Setup Variables
- `data_charges`: This variable is a dictionary that contains input data related to charges. It has four keys: "ENTITY", "SCENARIO", "LABEL", and "VALUE". The values associated with each key are lists that provide information about the entities, scenarios, labels, and values of the charges respectively. In this example, all the keys have fixed values repeated for each item in the list.
- `html_output`: This variable stores the file name or path for the HTML output.
- `png_output`: This variable stores the file name or path for the PNG output.


```python
# Inputs
data_charges = {
    "ENTITY": ["Société X"] * 5,
    "SCENARIO": ["2022-12"] * 5,
    "LABEL": ["Charges 1", "Charges 2", "Charges 3", "Charges 4", "Charges 5"],
    "VALUE": [100, 200, 300, 400, 500],
}

# Outputs
html_output = "Charges_HorizontalBarchart.html"
png_output = "Charges_HorizontalBarchart.png"
```

## Model

### Récupération de la données "Charges"


```python
df_charges = pd.DataFrame(data_charges)
df_charges
```

### Visualise Charges

Long description of the function to visualise charges using a horizontal barchart from plotly.


```python
fig = go.Figure(
    go.Bar(
        x=df_charges["VALUE"],
        y=df_charges["LABEL"],
        orientation="h",
        text=df_charges["VALUE"],
        textposition="auto",
        marker=dict(color="#cd3244")
    )
)
total = "{:,.0f} €".format(df_charges['VALUE'].sum()).replace(",", " ")
fig.update_layout(
    title=f"Toal Charges : {total}",
    title_font=dict(family="Arial", size=18, color="black"),
    plot_bgcolor="#ffffff",
    xaxis_title=None,
    xaxis_showticklabels=False,
    yaxis_title=None,
    margin_pad=10,
    margin_l=150,
    bargap=0.1,  # gap between bars of adjacent location coordinates.
    bargroupgap=0.2,  # gap between bars of the same location coordinate.
)
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

 
