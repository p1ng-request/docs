<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Create_spinner_button.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Create+spinner+button:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #button #download #create #python #library #spinner

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create a spinner button with Dash. The `Spinner` component can be used inside buttons to indicate that an action is currently processing or taking place.



**References:**
- [Dash Bootstrap Components - Spinner](https://dash-bootstrap-components.opensource.faculty.ai/docs/components/spinner/)

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
from dash import html
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

### Create download button


```python
spinners = html.Div(
    [
        dbc.Button(
            dbc.Spinner(size="sm"),
            color="primary",
            disabled=True,
            className="me-1",
        ),
        dbc.Button(
            [dbc.Spinner(size="sm"), " Loading..."],
            color="primary",
            disabled=True,
        ),
    ]
)

app.layout = html.Div(
    [
        # SPACE
        html.Br(),
        
        # Spinner button
        spinners
    ]
)
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```

 
