<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Locate_city_on_map.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Locate+city+on+map:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #geocoding #city #coordinates #location #api

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get coordinates from a city name using Python and display it on a map.

**References:**
- [PyPI - Geocoder](https://pypi.org/project/geocoder/)

## Input

### Import libraries


```python
try:
    import geocoder
except:
    !pip install geocoder --user
    import geocoder
import pandas as pd
import plotly.express as px
```

### Setup Variables
- `city`: name of the city to get coordinates from
- `country`: name of the country to help find the city


```python
city = "Paris"
country = "France"
```

## Model

### Get coordinates from city

Using the `geocoder` library, we can get the coordinates from a city name.


```python
g = geocoder.arcgis(f"{city}, {country}")
lat, lng = g.latlng
df = pd.DataFrame([{"name": city, "latitude": lat, "longitude": lng, "size": 1}])
print(f"Coordinates of {city}: {lat}, {lng}")
```

## Output

### Locate city on map


```python
fig = px.scatter_mapbox(
    df,
    lat='latitude',
    lon='longitude',
    size='size',
    text='name',
    zoom=4,
    mapbox_style='open-street-map'
)
fig.update_layout(
    width=1200,
    height=800,
)
config = {"displayModeBar": False}
fig.show(config=config)
```

 
