    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FEC/FEC_Visualiser_Comparer_Ventes_Line_Chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FEC+-+Visualiser+Comparer+Ventes+Line+Chart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fec #plotly #naas #snippet #operations #linechart

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** Ce notebook vous permettra de visualiser et comparer les ventes de votre entreprise pour les périodes N et N-1 à l'aide de deux courbes de tendance. Vous pourrez facilement voir les tendances et les différences entre les deux périodes pour prendre des décisions éclairées pour améliorer vos ventes.

## Input

### Import libraries


```python
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import pandas as pd
import naas
import random
```

### Setup Variables


```python
# Inputs
# Create sample financial data
data_n = {
    "ENTITY": ["Société X"] * 12,
    "SCENARIO": ["2022-12"] * 12,
    "LABEL": [
        "Janvier",
        "Février",
        "Mars",
        "Avril",
        "Mai",
        "Juin",
        "Juillet",
        "Aout",
        "Septembre",
        "Octobre",
        "Novembre",
        "Décembre",
    ],
    "GROUP": ["N"] * 12,
    "VAR": [random.randint(5000, 12000) for i in range(0, 12)],
}
data_n_1 = {
    "ENTITY": ["Société X"] * 12,
    "SCENARIO": ["2022-12"] * 12,
    "LABEL": [
        "Janvier",
        "Février",
        "Mars",
        "Avril",
        "Mai",
        "Juin",
        "Juillet",
        "Aout",
        "Septembre",
        "Octobre",
        "Novembre",
        "Décembre",
    ],
    "GROUP": ["N-1"] * 12,
    "VAR": [random.randint(5000, 10000) for i in range(0, 12)],
}

# Outputs
html_output = "Ventes_Linechart.html"
png_output = "Ventes_Linechart.png"
```

## Model

### Get data 'année N'


```python
df_n = pd.DataFrame(data_n)
df_n.insert(loc=4, column="VALUE", value=df_n["VAR"].cumsum())
df_n
```

### Get "Cashout" data


```python
df_n_1 = pd.DataFrame(data_n_1)
df_n_1.insert(loc=4, column="VALUE", value=df_n_1["VAR"].cumsum())
df_n_1
```

### Create barlinechart using Plotly


```python
def create_linechart(
    df_n,
    df_n_1,
    xaxis_title=None,
    yaxis_title=None,
):
    # Create figure
    fig = go.Figure()

    # Add traces
    fig.add_trace(
        go.Scatter(
            name="N",
            x=df_n["LABEL"],
            y=df_n["VALUE"],
            marker=dict(color="blue"),
        )
    )
    fig.add_trace(
        go.Scatter(
            name="N-1",
            x=df_n_1["LABEL"],
            y=df_n_1["VALUE"],
            marker=dict(color="orange"),
        )
    )
    # Calc var
    last_n = df_n.loc[df_n.index[-1], "VALUE"]
    last_n_1 = df_n_1.loc[df_n_1.index[-1], "VALUE"]
    var = last_n - last_n_1
    if var > 0:
        var = f"+{var}"

    # Add figure title
    fig.update_layout(
        title=f"Ventes : {last_n} € ({var} € vs N-1)",
        title_font=dict(family="Arial", size=18, color="black"),
        legend=None,
        plot_bgcolor="#ffffff",
        width=1200,
        height=800,
        paper_bgcolor="white",
        xaxis_title=xaxis_title,
        xaxis_title_font=dict(family="Arial", size=12, color="black"),
        xaxis={"type": "category"},
    )

    # Set y-axes titles
    fig.update_yaxes(
        title_text=yaxis_title,
        title_font=dict(family="Arial", size=12, color="black"),
    )
    fig.show()
    return fig


fig = create_linechart(
    df_n,
    df_n_1,
    xaxis_title="Mois",
    yaxis_title="Valeur en €",
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
