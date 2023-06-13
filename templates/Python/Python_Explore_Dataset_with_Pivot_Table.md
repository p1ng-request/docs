<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Explore_Dataset_with_Pivot_Table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Explore+Dataset+with+Pivot+Table:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #dataset #pivottable #dataexploration

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook allows you to interactively explore and analyze a dataset using a pivot table. It uses the `pivottablejs` library to generate a dynamic pivot table in your web browser, giving you the ability to sort, filter, and aggregate data in real-time. This template provides a simple and intuitive way to explore and gain insights from your dataset, making it a valuable tool for data analysis and visualization.

<u>References:</u>
- https://github.com/nicolaskruchten/jupyter_pivottablejs
- https://github.com/nicolaskruchten/pivottable

## Input

### Import libraries


```python
import pandas as pd
try:
    from pivottablejs import pivot_ui
except:
    !pip install pivottablejs --user
    from pivottablejs import pivot_ui
```

### Setup Variables


```python
# Create a fake dataset
data = {
    "Month": [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
    ]
    * 2,
    "Region": ["North"] * 12 + ["South"] * 12,
    "Sales": [
        11000,
        12000,
        13000,
        14000,
        15000,
        16000,
        17000,
        18000,
        19000,
        20000,
        21000,
        22000,
    ]
    + [
        10000,
        11000,
        12000,
        13000,
        14000,
        15000,
        16000,
        17000,
        18000,
        19000,
        20000,
        21000,
    ],
}
```

## Model

### Create DataFrame


```python
df = pd.DataFrame(data)
df.head(12)
```

## Output

### Use the pivot_ui function to create a pivot table


```python
# Use the pivot_ui function to create a pivot table
pivot_ui(df)
```
