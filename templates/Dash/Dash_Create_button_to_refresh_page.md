<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Dash/Dash_Create_button_to_refresh_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Dash+-+Create+button+to+refresh+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #dash #python #button #refresh #page #stackoverflow

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook explains how to create a button in Dash to refresh the page.

**References:**
- [Dash Application Python Button for Refresh the Page](https://stackoverflow.com/questions/60762890/dash-application-python-button-for-refresh-the-page)

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

### Create button to refresh page


```python
app.layout = html.Div([
    # represents the browser address bar and doesn't render anything
    dcc.Location(id='url', refresh=False),

    dcc.Link('Navigate to "/"', href='/'),

    # content will be rendered in this element
    html.Div(id='page-content')
])


@app.callback(
    Output('page-content', 'children'),
    [Input('url', 'pathname')])
def display_page(relative_pathname):
    return html.Div([
        html.H3(f'You are on page {relative_pathname}'),
        html.A(html.Button('Refresh Page'),href=relative_pathname),
    ])
```

## Output

### Generate URL and show logs


```python
if __name__ == "__main__":
    app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
```


```python

```
