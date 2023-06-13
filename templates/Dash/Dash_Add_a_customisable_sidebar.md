<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Add_a_customisable_sidebar.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Add+a+customisable+sidebar:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #offcanvas #sidebar #customisable #component #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook demonstrates how to use the Offcanvas component to add a customisable sidebar to your apps. It is usefull for organisations that need to add a sidebar to their Dash apps.

**References:**
- [Dash Bootstrap Components - Offcanvas](https://dash-bootstrap-components.opensource.faculty.ai/docs/components/offcanvas/)
- [Dash Bootstrap Components - Getting Started](https://dash-bootstrap-components.opensource.faculty.ai/docs/getting-started)

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
from dash import Input, Output, State, html
```

### Setup Variables
- `DASH_PORT`: specify a port number for Dash
- `placement`: a value equal to: 'start', 'end', 'top', 'bottom'; optional: Which side of the viewport the offcanvas will appear from.


```python
DASH_PORT = 8050
placement = "start"
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

### Create Offcanvas component

Long description of the function: The Offcanvas component is a customisable sidebar that can be used to add content to your Dash apps. It is created using the `dbc.Offcanvas` function.


```python
offcanvas = html.Div(
    [
        dbc.Button("Open Offcanvas", id="open-offcanvas", n_clicks=0),
        dbc.Offcanvas(
            html.P(
                "This is the content of the Offcanvas. "
                "Close it by clicking on the close button, or "
                "the backdrop."
            ),
            id="offcanvas",
            title="Title",
            is_open=False,
            placement=placement,
        ),
    ]
)

app.layout = html.Div(
    [
        offcanvas
    ]
)

@app.callback(
    Output("offcanvas", "is_open"),
    Input("open-offcanvas", "n_clicks"),
    [State("offcanvas", "is_open")],
)
def toggle_offcanvas(n1, is_open):
    if n1:
        return not is_open
    return is_open
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```

 
