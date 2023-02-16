<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AlphaVantage/AlphaVantage_Get_company_overview.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=AlphaVantage+-+Get+company+overview:+Error+short+description">Bug report</a>

**Tags:** #alphavantage #trading #market_data #investors #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides an overview of the AlphaVantage API, which allows users to access real-time and historical financial data for global equities, commodities, and currencies. It provides a comprehensive set of tools to analyze and visualize financial data for a variety of purposes.

## Input

### Import libraries


```python
import requests
import pandas as pd
```

### Variables


```python
API_KEY = "demo"
COMPANY = "IBM"
```

## Model

### Get company overview


```python
response = requests.get(
    f"https://www.alphavantage.co/query?function=OVERVIEW&symbol={COMPANY}&apikey={API_KEY}"
)
data = response.json()
```

## Output

### Display result


```python
data
```
