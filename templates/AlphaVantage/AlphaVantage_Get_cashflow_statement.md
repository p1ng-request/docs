<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AlphaVantage/AlphaVantage_Get_cashflow_statement.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=AlphaVantage+-+Get+cashflow+statement:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #alphavantage #trading #market_data #investors #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides a way to access financial data from AlphaVantage, including cashflow statements.

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

### Get cashflow statement


```python
response = requests.get(
    f"https://www.alphavantage.co/query?function=CASH_FLOW&symbol={COMPANY}&apikey={API_KEY}"
)
data = response.json()
df = pd.DataFrame(data.get("annualReports"))
```

## Output

### Display result


```python
df
```
