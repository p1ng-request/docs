<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FAO/FAO_Consumer_price_indice.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FAO+-+Consumer+price+indice:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fao #opendata #food #analytics #plotly

**Author:** [Dereck DANIEL](https://github.com/DANIEL-Dereck)

**Description:** This notebook provides an analysis of the changes in consumer prices over time as measured by the Food and Agriculture Organization's Consumer Price Index.

## Input

### Import librairies


```python
import requests, zipfile, io
import matplotlib.pyplot as plt
import naas_drivers
import pandas as pd
import plotly.express as px
import csv
import codecs
import plotly.graph_objects as go
```

### Set the variables


```python
filename = "ConsumerPriceIndices_E_All_Data_(Normalized).csv"
zip_file_url = "http://fenixservices.fao.org/faostat/static/bulkdownloads/ConsumerPriceIndices_E_All_Data_(Normalized).zip"
```

### Get the data


```python
r = requests.get(zip_file_url, stream=True)
z = zipfile.ZipFile(io.BytesIO(r.content))
z.extractall()

df = pd.read_csv(filename, encoding="latin-1")
df.to_csv(filename, index=False)
df = pd.read_csv(filename)

df.head()
```

## Model

### Sort the data


```python
df = df[df["Item Code"] == 23013]
df = df[df.Year == 2020]
dfmax10 = (
    df.groupby(["Area", "Year"])
    .mean()
    .reset_index()
    .sort_values("Value", ascending=False)
    .reset_index()
)
dfmin10 = (
    df.groupby(["Area", "Year"])
    .mean()
    .reset_index()
    .sort_values("Value", ascending=True)
    .reset_index()
)
```

## Output

### Display the plot of the Top 10 of the biggest evolution in 2020


```python
dfmax10y = dfmax10["Area"].head(10).iloc[::-1]
dfmax10x = dfmax10["Value"].head(10).iloc[::-1]

fig = go.Figure(go.Bar(x=dfmax10x, y=dfmax10y, orientation="h"))

fig.update_xaxes(type="log")
fig.update_layout(title_text="Top 10 of the biggest evolution in 2020")

fig.show()
```

### Display the plot of the Top 10 of the worst evolution in 2020


```python
dfmin10y = dfmin10["Area"].head(10).iloc[::-1]
dfmin10x = dfmin10["Value"].head(10).iloc[::-1]

fig = go.Figure(go.Bar(x=dfmin10x, y=dfmin10y, orientation="h"))

fig.update_layout(title_text="Top 10 of the worst evolution in 2020")
fig.show()
```
