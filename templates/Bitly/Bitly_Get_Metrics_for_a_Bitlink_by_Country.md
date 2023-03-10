<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Metrics_for_a_Bitlink_by_Country.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Metrics+for+a+Bitlink+by+Country:+Error+short+description">Bug report</a>

**Tags:** #bitly #api #metrics #bitlink #country #reference

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use the Bitly API to get metrics for a Bitlink by Country.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getMetricsForBitlinkByCountries)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
import plotly.graph_objects as go
try:
    from dataprep.clean import clean_country
except:
    !pip install dataprep --user
    from dataprep.clean import clean_country
import json
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)
```

### Setup Variables
- **access_token**: [Generate an access token](https://dev.bitly.com/authentication.html)
- **bitlink**: The Bitlink for which you want to get metrics


```python
# Inputs
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN>"
bitlink = "bit.ly/3lU6hRt"
title = "Bitly - Get Metrics for a Bitlink by Country"

# Outputs
output_image = f"{title}.png"
output_html = f"{title}.html"
```

## Model

### Get Metrics for a Bitlink by Country

This function will use the Bitly API to get metrics for a Bitlink by Country.


```python
def get_metrics_by_country(access_token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/countries"
    headers = {"Authorization": f"Bearer {access_token}"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return json.loads(response.content)
    else:
        return None
    
metrics_by_country = get_metrics_by_country(access_token, bitlink)
```

### Prep Data


```python
def prep_data(data):
    # Init
    df = pd.DataFrame(data)
    
    # Cleaning
    to_rename = {
        "value": "COUNTRY",
        "clicks": "VALUE"
    }
    df = df.rename(columns=to_rename)
    
    # Get countries
    df = clean_country(df, "COUNTRY", output_format="alpha-3").dropna().rename(columns={"COUNTRY_clean": "COUNTRY_ISO"})
    df = clean_country(df, "COUNTRY", output_format="name").dropna().rename(columns={"COUNTRY_clean": "COUNTRY_NAME"})              
    return df

df = prep_data(metrics_by_country.get("metrics"))
df
```

### Create Worlmap


```python
fig = go.Figure()

fig = go.Figure(
    data=go.Choropleth(
        locations=df["COUNTRY_ISO"],
        z=df["VALUE"].astype(int),
        text=df["COUNTRY_NAME"],
        colorscale="Oranges",
        autocolorscale=False,
        reversescale=False,
        marker_line_color="darkgray",
        marker_line_width=0.5,
        colorbar_tickprefix="",
        colorbar_title="Clicks",
    )
)

fig.update_layout(
    title=title,
    plot_bgcolor="#ffffff",
    legend_x=1,
    geo=dict(
        showframe=False,
#         showcoastlines=False,
    ),
    dragmode=False,
    width=1200,
    height=800,
)

config = {"displayModeBar": False}
fig.show(config=config)
```

## Output

### Export in PNG and HTML


```python
fig.write_image(output_image, width=1200)
fig.write_html(output_html)
```

### Generate shareable assets


```python
link_image = naas.asset.add(output_image)
link_html = naas.asset.add(output_html, {"inline": True})

# -> Uncomment the line below to remove your assets
# naas.asset.delete(output_image)
# naas.asset.delete(output_html)
```

 
