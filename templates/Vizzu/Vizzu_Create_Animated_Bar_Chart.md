<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Vizzu/Vizzu_Create_Animated_Bar_Chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Vizzu+-+Create+Animated+Bar+Chart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #vizzu #animation #bar-chart #data-visualization #data-science #python

**Author:** [Alexandre Petit](https://www.linkedin.com/in/alexandre-petit-24a87a219/)

**Description:** This notebook would allow you to create an animated bar chart. It will show the oil production evolution by country year after year.

**References:**
- https://ipyvizzu.vizzuhq.com/latest/showcases/musicformats/
- https://ipyvizzu.vizzuhq.com/latest/examples/animation/

## Input

### Import libraries


```python
import naas
import pandas as pd
try:
    from ipyvizzu import Chart, Data, Config, Style, DisplayTarget
except:
    !pip install ipyvizzu --user
    from ipyvizzu import Chart, Data, Config, Style, DisplayTarget
```

### Setup Variables
- `file_path`: url to the csv file
- `category`: the column representing each bar
- `value`: the column with the values 
- `time_col`: the column of the time period
- `labels`: a list of labels that will be displayed in the animated bar chart
- `labels_color`: a list of hexadecimal color by labels. If len is not the same as labels then it will reuse the first colors
- `html_output`: The file path where the HTML output file should be created.


```python
# Inputs
file_path = "https://raw.githubusercontent.com/alexandre-petit/oil-production/main/oil-production-by-country.csv"
category = "Entity"
value = "Oil production (TWh)"
time_col = "Year"
labels = [
    'United States',
    'Russia',
    'USSR',
    'Venezuela',
    'Saudi Arabia',
    'Canada',
    'Brazil',
    'Iraq',
    'China',
    'United Arab Emirates',
    'Iran',
    'Algeria'
]
labels_color = [
    "#b74c20FF",
    "#c47f58FF",
    "#1c9761FF",
    "#ea4549FF", 
    "#875792FF",
    "#3562b6FF",
    "#ee7c34FF",
    "#efae3aFF"
]

# Outputs
html_output = "Vizzu_Create_Animated_Bar_Chart.html"
```

## Model

### Get data from csv


```python
df = pd.read_csv(file_path)
# Cleaning
df[category] = df[category].astype(str)
df[value] = df[value].astype(float)
df
```

### Create Animated Bar Chart

This function will create an animated bar chart to show the oil production evolution by country year after year.


```python
# Add data to Chart
data = Data()
data.add_data_frame(df[df[category].isin(labels)])

# Adding the config
config = {
    "channels": {
        "y": {
            "set": [category],
        },
        "x": {"set": [value]},
        "label": {"set": [value]},
        "color": {"set": [category]}, #if the color column is different than y column, both columns needs to be passed as a parameter for y
    },
    "sort": "byValue",
}

# Colors, labels, padding
style = Style(
    {
        "plot": {
            "paddingLeft": 100,
            "paddingTop": 25,
            "yAxis": {
                "color": "#ffffff00",
                "label": {"paddingRight": 10},
            },
            "xAxis": {
                "title": {"color": "#ffffff00"},
                "label": {
                    "color": "#ffffff00",
                    "numberFormat": "grouped",
                },
            },
            "marker": {
                #colorPalette take a string of hexadecimal color separated by a whitespace
                #for simplicity, we will join the list of hexadecimal color defined before
                "colorPalette": " ".join(labels_color)

            },
        },
    }
)

# Initialize Chart
chart = Chart(width="640px", height="360px", display=DisplayTarget.MANUAL)
chart.animate(data, style)

# Get time range
min_time = df[time_col].min()
max_time = df[time_col].max()

# This part is looping over the time period
for year in range(min_time, max_time + 1):
    config["title"] = f"Oil Production in {year}"
    chart.animate(
        Data.filter(f"parseInt(record.{time_col}) == {year}"),
        Config(config),
        duration=1,
        x={"easing": "linear", "delay": 0},
        y={"delay": 0},
        show={"delay": 0},
        hide={"delay": 0},
        title={"duration": 0, "delay": 0},
    )

# display Chart
chart.show()
```

## Output

### Export chart in HTML


```python
chart._showed = False
rawhtml = chart._repr_html_()

with open(html_output, "w", encoding="utf8") as file_desc:
    file_desc.write(rawhtml)
```

 
