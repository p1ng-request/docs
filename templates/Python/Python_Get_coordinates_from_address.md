    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Get_coordinates_from_address.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Get+coordinates+from+address:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #snippet #naas #geocoder

**Author:** [Suhas B](https://www.linkedin.com/in/suhasbrao/)

**Description:** This notebook get coordinates from a given address.

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
```

### Setup Variables


```python
# sample address to geo code
address = "Sayyaji Rao Rd, Agrahara, Chamrajpura, Mysuru, Karnataka 570001"
```

## Model

### Get data from geocoder


```python
geo = geocoder.arcgis(address)
```

## Output

### Display latitude and longitude from address


```python
latitude_and_longitude = geo.latlng
print(f"Latitude and Longitude of given address '{address}':\n{latitude_and_longitude}\n")

# If we want to retrieve the location from a set of coordinates
# perform a reverse query.

location_from_coordinates = geocoder.arcgis(latitude_and_longitude, method="reverse")
print(f"Location from coordinates:\n{location_from_coordinates[0]}")
```
