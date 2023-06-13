<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WAQI/WAQI_Get_daily_air_quality_data_by_coordinates.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WAQI+-+Get+daily+air+quality+data+by+coordinates:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #waqi #airquality #api #data #city #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use the WAQI API to get daily air quality data for a city.

**References:**
- [WAQI API Documentation](https://aqicn.org/json-api/doc/)
- [Air Quality Index Scale](https://aqicn.org/scale/)

## Input

### Import libraries


```python
import requests
import naas
import pydash
from pprint import pprint
```

### Setup Variables
- `token`: WAQI API token. [Get your token here](https://aqicn.org/data-platform/token/).
- `lat`: Latitude
- `lng`: Longitude


```python
# Inputs
token = naas.secret.get("WAQI_TOKEN") or "YOUR_TOKEN_HERE"
lat = 48.856614
lng = 2.3522219
```

## Model

### Get daily air quality data
This function will use the WAQI API to get daily air quality data for a latitude and longitude.


```python
def get_daily_air_quality_data(token, lat, lng):
    url = f"https://api.waqi.info/feed/geo:{lat};{lng}?token={token}"
    res = requests.get(url)
    if res.status_code == 200:
        return res.json()

data = get_daily_air_quality_data(token, lat, lng)
```

## Output

### Display result


```python
city = pydash.get(data, "data.city.name")
aqi = pydash.get(data, "data.aqi")
date = pydash.get(data, "data.time.s")
print(f"☝️ {city} - Air Quality Index:", aqi)
print("⏱️ Date extract:", date)
pprint(data)
```

 
