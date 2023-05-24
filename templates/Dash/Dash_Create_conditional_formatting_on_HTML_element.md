<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Create_conditional_formatting_on_HTML_element.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Create+conditional+formatting+on+HTML+element:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #html #conditional #formatting #element #plotly

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create conditional formatting of an HTML element using Dash.

**References:**
- https://community.plotly.com/t/conditional-formatting-of-an-html-element/60230/2
- https://dash.plotly.com/

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
from dash import html, dcc, Output, Input, State
```

### Setup Variables
- `DASH_PORT`: specify a port number for Dash


```python
DASH_PORT = 8050
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

### Create app layout


```python
app.title = "Naas"
app.layout = html.Div(
    [
        html.H1("Enter your color in HEX"),
        dcc.Input(id="input"),
        html.H4(id="heading", children="A Heading")
    ]
)

@app.callback(
    Output("heading", "style"),
    Input("input", "value")
)
def update_style(value):
    return {
        "color": value
    }
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```


```python

```
