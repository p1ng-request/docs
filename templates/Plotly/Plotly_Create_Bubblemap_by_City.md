    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Plotly_Create_Bubblemap_by_City.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Plotly+-+Create+Bubblemap+by+City:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #plotly #bubblemap #city #python #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to creates a bubblemap with values by city using Plotly.

**References:**
- [Plotly Bubble map](https://plotly.com/python/bubble-maps/)
- [Plotly Choropleth Maps](https://plotly.com/python/choropleth-maps/)

## Input

### Import libraries


```python
import pandas as pd
import plotly.express as px
import naas
```

### Setup Variables
- `file_path`: file path containing cities with latitude and longitude
- `output_html`: html output path


```python
# Inputs
file_path = 'https://raw.githubusercontent.com/R-CoderDotCom/data/main/sample_datasets/population_spain.csv'

# Outputs
output_html = f"Bubblemap.html"
```

## Model

### Get data with latitude/longitude and values


```python
df = pd.read_csv(file_path, encoding ='latin-1')
print("Row fetched:", len(df))
df.head(5)
```

### Create Bubblemap


```python
fig = px.scatter_mapbox(
    df,
    lat='latitude',
    lon='longitude',
    size='tot_pop',
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

## Output

### Export HTML


```python
fig.write_html(output_html)
```

### Generate shareable asset


```python
link_html = naas.asset.add(output_html, {"inline": True})

# -> Uncomment the line below to remove your assets
# naas.asset.delete(output_html)
```

 
