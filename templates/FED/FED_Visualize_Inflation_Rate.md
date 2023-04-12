<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/FED/FED_Visualize_Inflation_Rate.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=FED+-+Visualize+Inflation+Rate:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #fed #inflation_rate #vizualization #plotly

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook vizualize the inflation rate of the US using plotly and fred api

## Input


```python
import naas
import pandas as pd
import plotly.express as px
# fredapi
try:
    from fredapi import Fred
except ModuleNotFoundError:
    !pip install fredapi
    from fredapi import Fred
```

### Setup Variables
- `fred_api_key`: Fred API Key, to obtain an Fred API key, please refer to the [St. Louis Fed Website](https://fred.stlouisfed.org/).
- `series_id`: A series ID is used to retrieve data for a specific economic indicator from the FRED database, please refer to the [FRED Documentation](https://fred.stlouisfed.org/docs/api/fred/#General_Documentation)


```python
## api key
fred_api_key = naas.secret.get("FRED_API_KEY")
```


```python
## series id
series_id = 'CPALTT01USM657N'
```


```python
## initialize Fred with api key
fred = Fred(api_key=fred_api_key)
```


```python
# Define the start date for the inflation rate data
start_date = "1960-01-01"
```


```python
# Retrieve the inflation rate data
data = fred.get_series(series_id, start_date)
```

## Model


```python
# Convert the data to a Pandas DataFrame
df = pd.DataFrame(data, columns=["inflation rate"])
```


```python
# Resample the data to the annual frequency and calculate the mean
df = df.resample("A").mean()
```


```python
# Create a line plot using Plotly
fig = px.line(df, x=df.index, y="inflation rate", title="US Inflation Rate (1960-2023)")
```

## Output


```python
## display the plot
fig.show()
```
