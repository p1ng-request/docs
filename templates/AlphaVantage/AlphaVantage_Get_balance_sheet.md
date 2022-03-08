<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AlphaVantage/AlphaVantage_Get_balance_sheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #trading #market_data

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

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
response = requests.get(f'https://www.alphavantage.co/query?function=BALANCE_SHEET&symbol={COMPANY}&apikey={API_KEY}')
data = response.json()
df = pd.DataFrame(data.get("annualReports"))
```

## Output

### Display result


```python
df
```
