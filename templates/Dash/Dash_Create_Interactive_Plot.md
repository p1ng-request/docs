<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Create_Interactive_Plot.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Create+Interactive+Plot:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #dashboard #plotly #naas #asset #analytics #dropdown #callback #bootstrap #snippet

**Author:** [Zihui Ouyang](https://www.linkedin.com/in/zihui-ouyang-539626227/)

**Description:** This notebook creates an interactive plot using Dash app infrastructure.

**References:**
- https://stackoverflow.com/questions/70886359/dash-python-making-subplots-when-multiple-parameters-are-selected
- https://dash-example-index.herokuapp.com/line-charts

## Input

### Import libraries


```python
import os
try:
    import dash
except:
    !pip install dash --user
    import dash
try:
    import dash_bootstrap_components as dbc
except:
    !pip install dash_bootstrap_components --user
    import dash_bootstrap_components as dbc
import pandas as pd
from dash import Dash, html, dcc, callback, Output, Input
import plotly.express as px
import io
import requests
```

### Setup Variables
- `DASH_PORT`: specify a port number for Dash
- `url`: URL to get data from csv


```python
DASH_PORT = 8050
url = "https://covid.ourworldindata.org/data/owid-covid-data.csv?v=2023-04-30"
```

## Model

### Initialize Dash app


```python
app = dash.Dash(
    requests_pathname_prefix=f'/user/{os.environ.get("JUPYTERHUB_USER")}/proxy/{DASH_PORT}/',
    external_stylesheets=[dbc.themes.BOOTSTRAP],
    meta_tags=[
        {"name": "viewport", "content": "width=device-width, initial-scale=1.0"}
    ],
)

# app = dash.Dash() if you are not in Naas
```

### Get data


```python
r = requests.get(url).content
contents_df = pd.read_csv(io.StringIO(r.decode('utf-8')))
contents_df.head(1)
```

### Create Dash App


```python
PS = ["new_cases_smoothed", "new_deaths_smoothed"] # list that helps to create subplots

app.layout = html.Div(
    [
        html.H4("New Covid Cases and deaths per day"),
        html.P("Select countries"),
        dcc.Dropdown(
            id="countries",
            options=contents_df.location.unique(),
            value=["World"],
            multi = True
        ),
        *[dcc.Graph(id=p, figure={}, style={'display': 'none'}) for p in PS]
    ]
)

@callback(
    [Output(p, 'figure') for p in PS],
    [Output(p, 'style') for p in PS],
    Input('countries', 'value')
)

def update_graph(country):
    dff = contents_df.location.isin(country)
    figures = [{} for _ in range(len(PS))]
    styles = [{'display': 'none'} for _ in range(len(PS))]
    for i in range(2):
        figures[i] = px.line(contents_df[dff], x='date', y=PS[i], color = "location")
        styles[i]['display'] = 'block'    
    return *figures, *styles
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```


```python

```
