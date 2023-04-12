    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Locate_coordinates.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Locate+coordinates:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #snippet #naas #geocoder

**Author:** [Suhas B](https://www.linkedin.com/in/suhasbrao/)

**Description:** This notebook provides a way to find the geographic coordinates of a given location using Python.

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
latitude = 12.30215530579874
longitude = 76.65306751341747
```

## Model

### Get location from coordinates


```python
location_from_coordinates = geocoder.arcgis([latitude, longitude], method="reverse")
```

## Output

### Display location from coordinates


```python
print(f"Location from coordinates: {location_from_coordinates[0]}")
```
