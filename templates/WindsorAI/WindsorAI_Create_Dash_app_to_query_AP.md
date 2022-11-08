<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WindsorAI/WindsorAI_Create_Dash_app_to_query_AP.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WindsorAI+-+Create+Dash+app+to+query+AP:+Error+short+description">Bug report</a>

**Tags:** #tool #naas_drivers #naas #dash #marketing #automation #ai #analytics

**Author:** [Elia Dabbas](https://www.linkedin.com/in/eliasdabbas/)

**Description:** This notebook enable anyone with a [Windsor.ai](https://windsor.ai/) account to visualy query the API with a Dash app.

## Input

### Import packages


```python
pip install dash_bootstrap_templates
```

### Import libraries


```python
import json
import os
import requests
import pandas as pd
import plotly.express as px
from dash import Dash, html, dcc, Input, Output, State, callback
from dash.dash_table import DataTable
from dash.exceptions import PreventUpdate
from jupyter_dash import JupyterDash
import dash_bootstrap_components as dbc
from dash_bootstrap_templates import load_figure_template
load_figure_template('flatly')

pd.options.display.max_columns = None
```

### Parameters


```python
KNATIVE = False
```

### Defining key parameters and variables


```python
DASH_PORT = 8050

BASE_URL = 'https://connectors.windsor.ai/all'
PARAMS = dict(
    api_key = None,
    date_preset = None,
    fields = None,
)

date_preset_options = {
    'Yesterday': 'last_1d',
    'Last 3 days': 'last_3d',
    'Last 7 days': 'last_7d',
    'Last 14 days': 'last_14d',
    'Last 28 days': 'last_28d',
    'Last 30 days': 'last_30d',
    'Last 90 days': 'last_90d',
    'Last 180 days': 'last_180d',
    'This month': 'this_month',
    '1 year': 'last_year'
}

# to implement custom dates, this format can be used:
# date_from=2021-10-05&date_to=2021-10-08

fields_options = [
    'account_name',
    'campaign',
    'clicks',
    'countryisocode',
    'datasource',
    'date',
    'email',
    'flat_file_open_listings_data__asin',
    'sessions',
    'source',
    'spend',
]
```

## Model

### Helper functions


```python
def make_table(df):
    table = DataTable(
        data=df.to_dict('records'),
        columns=[{'name': i, 'id': i } for i in df.columns],
        style_header={
            'fontFamily': 'Arial',
            'fontColor': '#2F3B4C',
            'fontWeight': 'bold'},
        style_data={'fontFamily': 'Arial'},
        style_cell={
            'overflow': 'hidden',
            'textOverflow': 'ellipsis',
            'minWidth': 100},
        virtualization=True,
        sort_action='native',
        page_size=500,
        fixed_rows={'headers': True},
        export_format='csv',
        )
    return table


def num_cols(df):
    numeric_cols = []
    for col in df:
        try:
            df[col].astype(float)
            numeric_cols.append(col)
        except:
            continue
    return numeric_cols
```

### Instantial app and create app's layout


```python
if KNATIVE is False:
    app = Dash(
        requests_pathname_prefix=f'/user/{os.environ.get("JUPYTERHUB_USER")}/proxy/{DASH_PORT}/',
        external_stylesheets=[dbc.themes.FLATLY])
else:
    app = Dash(
        external_stylesheets=[dbc.themes.FLATLY])


app.layout = html.Div([
    dcc.Store(id='store_columns'),
    html.Br(), html.Br(),
    html.H2([html.B("windsor.ai"),
             html.Span(" – interactive dashboard")],
            style={'textAlign': 'center'}), html.Br(),
    dbc.Row([
        dbc.Col(lg=1),
        dbc.Col([
            dbc.Label('Date range:'),
            dcc.Dropdown(
                id='date_dropdown',
                value='last_7d',
                options=[{'label': k, 'value': v}
                         for k, v in date_preset_options.items()]), html.Br(),
        ], lg=2),
        dbc.Col([
            dbc.Label('Fields:'),
            dcc.Dropdown(
                id='fields_dropdown',
                multi=True,
                options=[{'label': field.replace('_', ' ').title(),
                          'value': field}
                         for field in fields_options]), html.Br(),
        ], lg=4),
        dbc.Col([
            dbc.Label('Your API key:'),
            dbc.Input(id='api_key')
        ], lg=2),
        dbc.Col([
            html.Br(),
            html.Div(dbc.Button('Submit', id='submit_button'),
                     )
        ], lg=2),
    ]), html.Hr(), html.Br(),
    dbc.Row([
        dbc.Col(lg=1),
        dbc.Col([
            html.Div([
                dbc.Col([dcc.Dropdown(id='num_cols_dropdown')], lg=3)
                ,
                dcc.Loading(dcc.Graph(id='chart')), html.Br(),
                dcc.Loading(html.Div(id='output'))
            ], hidden=True, id='output_id')
        ], lg=10),
    ])
])
```

### Create app's callback function/interactivity


```python
@app.callback(
    Output('output', 'children'),
    Output('num_cols_dropdown', 'options'),
    Output('output_id', 'hidden'),
    Output('store_columns', 'data'),
    Input('submit_button', 'n_clicks'),
    State('date_dropdown', 'value'),
    State('fields_dropdown', 'value'),
    State('api_key', 'value'),
    prevent_initial_call=True)
def make_api_request(n_clicks, date_dropdown, fields_dropdown, api_key):
    if 'date' not in fields_dropdown:
        fields_dropdown.append('date')
    PARAMS['date_preset'] = date_dropdown
    PARAMS['fields'] = ','.join(fields_dropdown)
    PARAMS['api_key'] = api_key
    response = requests.get(BASE_URL, params=PARAMS)
    resp_df = pd.DataFrame(response.json()['data'])
    table = make_table(resp_df)
    hidden = False
    return table, num_cols(resp_df), hidden, resp_df.to_json()


@app.callback(
    Output('chart', 'figure'),
    Input('num_cols_dropdown', 'value'),
    Input('store_columns', 'data'),
    prevent_initial_call=True)
def make_chart(value, data):
    if not value:
        raise PreventUpdate
    df = pd.DataFrame.from_dict(json.loads(data))
    for col in df:
        try:
            df[col] = df[col].astype(float)
        except:
            continue
    dftest = df
    fig = px.bar(
        df.groupby('date').sum().reset_index(), x='date', y=value, title=f'<b>Total daily {value}</b>')
    return fig

```

## Output

### Run the Dash app server


```python
if __name__ == '__main__':
    if KNATIVE is False:
        app.run_server(proxy=f"http://127.0.0.1:{DASH_PORT}::https://app.naas.ai")
    else:
        app.run_server()

```
