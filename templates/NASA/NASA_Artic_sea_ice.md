# NASA - Artic sea ice
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/NASA/NASA_Artic_sea_ice.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #opendata

AVERAGE SEPTEMBER MINIMUM EXTENT<br>
Data source: Satellite observations. Credit: NSIDC/NASA

**What is Arctic sea ice extent?**<br>
Sea ice extent is a measure of the surface area of the ocean covered by sea ice. Increases in air and ocean temperatures decrease sea ice extent; in turn, the resulting darker ocean surface absorbs more solar radiation and increases Arctic warming.<br>
Date Range: 1979 - 2020.

## Get data from website
https://climate.nasa.gov/ => click on Artic Sea Ice

## Input

### Import libraries


```python
import pandas
import plotly.express as px
```

## Model

### Read the csv


```python
df = pandas.read_csv("https://climate.nasa.gov/system/internal_resources/details/original/2264_N_09_extent_v3.0.csv")

df.head(5)#read the first 5 lines
```

## Ouput

### Create simple graph


```python
fig = px.line(df, x="year", y=" extent")
fig.show()
```
