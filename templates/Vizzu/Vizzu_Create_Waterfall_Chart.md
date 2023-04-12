<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Vizzu/Vizzu_Create_Waterfall_Chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Vizzu+-+Create+Waterfall+Chart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #analytics #dataviz #chart #graph #waterfallChart

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel/)

**Description:** This notebook template on Vizzu is designed to help users create visually appealing waterfall charts. Vizzu is a powerful data visualization tool that allows users to easily create interactive and engaging charts and graphs

**References:**
- [Vizzu Waterfall Chart](https://ipyvizzu.vizzuhq.com/latest/examples/presets/08_C_R_waterfall/)

## Input

### Import libraries


```python
import naas
import pandas as pd
try:
    from ipyvizzu import Chart, Data, Config, Style
except:
    !pip install ipyvizzu --user
    from ipyvizzu import Chart, Data, Config, Style
```

### Setup Variables
- `file_path`: The file path of the CSV file containing the data.
- `title`: The title to be displayed at the top of the chart.
- `label`: The name of the column to be used for the x-axis labels. The column type must be a `str`
- `group`: The name of the column that grouped the labels.
- `value`: The name of the column to be used for the y-axis values. The column type must be either `int` or `float`.
- `html_output`: The file path where the HTML output file should be created.


```python
# Inputs
file_path = "https://ipyvizzu.vizzuhq.com/0.15/assets/data/chart_types_eu.csv"
title = "Waterfall Chart"
label = "Year"
group = None
value = "Value 5 (+/-)"

# Outputs
html_output = "Vizzu_Create_Waterfall_Chart.html"
```

## Model

### Get data from csv


```python
df = pd.read_csv(file_path, dtype={label: str, group: str, value: float})
df
```

### Data Prep


```python
def prep_data(
    df,
    label=None,
    group=None,
    value=None,
    agg="sum"
):
    # Init
    to_group = []
    to_agg = {}
    
    # Set column to group
    if label:
        to_group += [label]
    if group:
        to_group += [group]
    if value:
        to_agg = {value: 'sum'}
        
    # Prep data
    df = df.groupby(to_group, as_index=False).agg(to_agg)
    return df

df_prep = prep_data(df, label, group, value)
df_prep
```

### Generate chart


```python
# initialize Chart
chart = Chart(width="640px", height="360px", display="manual")

# add data to Chart
data = Data()
data.add_data_frame(df_prep)
chart.animate(data)
 
# add config to Chart
chart.animate(data)
chart.animate(
    Config.waterfall( 
        {
            "title": title,
            "x": label,
            "y": value,
        }
    ),
    Style(
        {
            "plot": {
                "marker": {
                    "colorGradient": "#ff001b 0,#ff001b 0.5,#47dd82 0.5,#47dd82 1",
                    "label": {"position": "top"},
                }
            }
        }
    ),
)

# add style to Chart
chart.animate(Style({"title": {"fontSize": 25}}))

# display Chart
chart.show()
```

## Output

### Export story to HTML


```python
chart._showed = False
rawhtml = chart._repr_html_()

with open(html_output, "w", encoding="utf8") as file_desc:
    file_desc.write(rawhtml)
```

### Create shareable asset with Naas


```python
naas.asset.add(html_output, params={"inline": True})
```
