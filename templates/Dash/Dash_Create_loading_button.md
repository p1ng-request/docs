<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Create_loading_button.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Create+loading+button:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #plotly #loading #button #python #web

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook explains how to create a loading button with Dash Plotly.

**References:**
- [Dash Loading States](https://dash.plotly.com/loading-states)
- [Plotly Loading Button](https://dash-bootstrap-components.opensource.faculty.ai/docs/components/spinner/)

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
from dash import Dash, html, dcc, callback, Output, Input, State
import time
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

### Create loading button


```python
loading_spinner = html.Div(
    [
        dbc.Button(
            "Load",
            id="loading-button",
            n_clicks=0,
            className="d-grid gap-2 col-6 mx-auto",
            style={"padding": "20px"}
        ),
        dbc.Spinner(html.Div(id="loading-output")),
    ]
)

app.layout = html.Div(
    [
        # SPACE
        html.Br(),
        
        # Loading spinner
        loading_spinner,
    ]
)
    

@app.callback(
    Output("loading-output", "children"), [Input("loading-button", "n_clicks")]
)
def load_output(n):
    if n:
        time.sleep(3)
        return f"Output loaded {n} times"
    return "Output not reloaded yet"
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```

 
