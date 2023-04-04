<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WAQI/WAQI_Get_stations_by_coordinates.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WAQI+-+Get+stations+by+coordinates:+Error+short+description">Bug report</a>

**Tags:** #waqi #airquality #api #data #city #stations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to get stations within a given lat/lng bounds.

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

df = pd.DataFrame(data)
```

## Output

### Display result


```python
print("➡️ Results found:", len(df))
df.head(5)
```

 
