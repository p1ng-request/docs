<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Vizzu/Vizzu_Create_Grouped_Column_Chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Vizzu+-+Create+Grouped+Column+Chart:+Error+short+description">Bug report</a>

**Tags:** #analytics #dataviz #chart #graph #groupedbarchart

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel/)

**Description:** This notebook template on Vizzu is designed to help users create visually appealing grouped column charts. Vizzu is a powerful data visualization tool that allows users to easily create interactive and engaging charts and graphs

**References:**
- [Vizzu Grouped Column Chart](https://ipyvizzu.vizzuhq.com/latest/examples/presets/03_C_R_grouped_column_negative/)

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
- `label`: The name of the column to be used for the x-axis labels. The column type must be a `str`.
- `group`: The name of the column that grouped the labels.
- `value`: The name of the column to be used for the y-axis values. The column type must be either `int` or `float`.
- `html_output`: The file path where the HTML output file should be created.


```python
# Inputs
file_path = "https://ipyvizzu.vizzuhq.com/0.15/assets/data/chart_types_eu_data_6.csv"
title = "Grouped Column Chart"
label = "Country"
group = "Joy factors"
value = "Value 5 (+/-)"

# Outputs
html_output = "Vizzu_Create_Grouped_Column_Chart.html"
```

## Model

### Get data from csv


```python
df = pd.read_csv(file_path, dtype={label: str, group: str, value: float})
df
```

### Generate chart


```python
# initialize Chart
chart = Chart(width="640px", height="360px", display="manual")

# add data to Chart
data = Data()
data.add_data_frame(df)
chart.animate(data)
 
# add config to Chart
chart.animate(data)
chart.animate(
    Config.groupedColumn(
        {
            "title": title,
            "x": label,
            "y": value,
            "groupedBy": group,
        }
    )
)

# add style to Chart
chart.animate(Style({"title": {"fontSize": 25}}))

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

### Create shareable asset with Naas


```python
naas.asset.add(html_output, params={"inline": True})
```


```python

```
