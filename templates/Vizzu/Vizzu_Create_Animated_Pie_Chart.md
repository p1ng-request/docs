<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Vizzu/Vizzu_Create_Animated_Pie_Chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Vizzu+-+Create+Animated+Pie+Chart:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #vizzu #animation #piechart #data #visualization #python

**Author:** [Alexandre Petit](https://www.linkedin.com/in/alexandre-petit-24a87a219/)

**Description:** This notebook will show how to create an animated pie chart with Vizzu. An animated pie chart can be useful for visualizing changes or transitions in categorical data over time.

**References:**
- [Vizzu Documentation](https://vizzu.io/docs/getting-started/introduction)
- [Vizzu Tutorials](https://vizzu.io/tutorials)

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
- `title`: what is the graph about? "in YYYY" will be added to the title
- `category`: the column with the categories that will be displayed on the plot
- `value`: the column with the value
- `time_col`: the column with the year
- `graph_type`: the type of graph ('pie' or 'donut')
- `categories_color`: a list of hexadecimal color in the RGBA format by category. If len is not the same as the number of categories selected then it will reuse the first colors.
- `select_data`: a list  with the categories to display, "all" will include all the category but it is not recommended to display more than five categories on the same figure.
- `html_output`: The file path where the HTML output file should be created


```python
#inputs
file_path = "https://raw.githubusercontent.com/alexandre-petit/oil-production/main/oil_production_pie_chart.csv"
title = "Oil Production"
category = "Entity"
value = "value"
time_col = "Year"
graph_type = "pie"
categories_color = [
    "#abababFF",
    "#ea4549FF",
    "#3562b6FF",
    "#1c9761FF",
]
select_data = [
    'Others',
    'Russia',
    'United States',
    'Saudi Arabia'
]

#outputs
html_output = "Vizzu_Create_Animated_Pie_Chart.html"
```

## Model

## Get data from csv


```python
df = pd.read_csv(file_path)

#cleaning
df[category] = df[category].astype(str)
df[value] = df[value].astype(float)

#selecting the data for the graph
if select_data == 'all':
    pass
else:
    data_filter = (df[category].isin(select_data))
    df = df[data_filter].copy()
    
df
```

### Create Animated Pie Chart

This function will create an animated pie chart with Vizzu.


```python
#Add data to chart
data = Data()
data.add_data_frame(df)

#setting the inner radius
if graph_type == 'donut':
    y_ratio = -80
else:
    y_ratio = 0

    
#choosing the columns
config = {
    "channels": {
        "x": {"set": [category, value]},
        "y": {"range": {"min": f"{y_ratio}%"}},
        "label": {"set": [category, value]},
        "color": {"set": [category]},
    },
    "sort": "byValue",
    "coordSystem": "polar"
}

#colors, labels, padding
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
                "colorPalette": " ".join(categories_color)

            },
        },
    }
)

#Initialize Chart
chart = Chart(width="640px", height="360px", display=DisplayTarget.MANUAL)
chart.animate(data, style)

#Get time range
min_date = df[time_col].min()
max_date = df[time_col].max()

# This part is looping over the time period
for year in range(min_date, max_date + 1):
    config["title"] = title + f" in {year}"
    chart.animate(
        Data.filter(f"parseInt(record.{time_col}) == {year}"),
        Config(config),
        duration=0.5,
        x={"easing": "linear", "delay": 0},
        y={"delay": 0},
        show={"delay": 0},
        hide={"delay": 0},
        title={"duration": 0, "delay": 0},
    )

#Display Chart
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

 
