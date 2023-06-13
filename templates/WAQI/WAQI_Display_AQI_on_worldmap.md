<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WAQI/WAQI_Display_AQI_on_worldmap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WAQI+-+Display+AQI+on+worldmap:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #waqi #airquality #api #data #city #stations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook displays AQI on worldmap.<br>

Air Quality Index Scale:
- 0 - 50: Good - Air quality is considered satisfactory, and air pollution poses little or no risk
- 51 - 100: Moderate - Air quality is acceptable; however, for some pollutants there may be a moderate health concern for a very small number of people who are unusually sensitive to air pollution.
- 101-150: Unhealthy for Sensitive Groups - Members of sensitive groups may experience health effects. The general public is not likely to be affected.
- 151-200: Unhealthy - Everyone may begin to experience health effects; members of sensitive groups may experience more serious health effects.
- 201-300: Very Unhealthy - Health warnings of emergency conditions. The entire population is more likely to be affected.
- 300+: Hazardous - Health alert: everyone may experience more serious health effects.

**References:**
- [WAQI API Documentation](https://aqicn.org/json-api/doc/#api-Map_Queries-GetMapStations)
- [Air Quality Index Scale](https://aqicn.org/scale/)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
import plotly.express as px
```

### Setup Variables
- `token`: WAQI API token. [Get your token here](https://aqicn.org/data-platform/token/).
- `latlng`: map bounds in the form lat1,lng1,lat2,lng2


```python
# Inputs
token = naas.secret.get("WAQI_TOKEN") or "YOUR_TOKEN_HERE"
latlng = "-90,-180,90,180"

# Outputs
output_html = "WAQI_worldmap.html"
output_csv = "WAQI_data.csv"
```

## Model

### Get all stations by lat/lng bounds


```python
def get_all_stations(token, latlng):
    url = f'https://api.waqi.info/map/bounds?token={token}&latlng={latlng}'
    res = requests.get(url)
    if res.status_code == 200:
        return res.json()

result = get_all_stations(token, latlng)
```

### Create dataframe


```python
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

data = []
for d in result.get("data"):
    aqi = d.get("aqi")
    if aqi != "-":
        station = flatten_dict(d, parent_key='', sep='_')
        data.append(station)

df = pd.DataFrame(data).reset_index(drop=True)

# Cleaning
df = df.astype({"aqi": int})

def set_color(row):
    hex_code = "" # example hexadecimal color code
    aqi = row["aqi"]
    if aqi <= 50:
        hex_code = '#009966'
    elif aqi <= 100:
        hex_code = '#ffde33'
    elif aqi <= 150:
        hex_code = '#ff9933'
    elif aqi <= 200:
        hex_code = '#cc0033'
    elif aqi <= 250:
        hex_code = '#660099'
    else:
        hex_code = '#7e0023'
    return hex_code
    # convert hexadecimal to RGB
    red = int(hex_code[1:3], 16)
    green = int(hex_code[3:5], 16)
    blue = int(hex_code[5:7], 16)

    rgb_code = (red, green, blue) # RGB tuple
    return rgb_code # output: (255, 165, 0)

df["color"] = df.apply(lambda row: set_color(row), axis=1)
print("➡️ Results found:", len(df))
df.head(5)
```

### Create Bubblemap


```python
fig = px.scatter_mapbox(
    df,
    lat='lat',
    lon='lon',
    size='aqi',
    color='color',
    color_discrete_map="identity",
    zoom=2,
    mapbox_style='carto-positron',
    text='station_name',
    hover_name="station_name",
)
fig.update_layout(
    title="World's Air Pollution: Real-time Air Quality Index",
    autosize=True,
)
config = {"displayModeBar": False}
fig.show(config=config)
```

## Output

### Save data in csv


```python
df.to_csv(output_csv, index=False)
```

### Export HTML


```python
fig.write_html(output_html)
```

### Generate shareable asset


```python
link_csv = naas.asset.add(output_csv, {"inline": True})
link_html = naas.asset.add(output_html, {"inline": True})

# -> Uncomment the line below to remove your assets
# naas.asset.delete(output_csv)
# naas.asset.delete(output_html)
```

 


```python

```
