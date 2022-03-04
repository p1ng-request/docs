<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# AlphaVantage - Get fundamental data
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AlphaVantage/AlphaVantage_Get_fundamental_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

#trading #market_data

## Company overview


```python
import requests
import pandas as pd

response = requests.get('https://www.alphavantage.co/query?function=OVERVIEW&symbol=IBM&apikey=demo')
data = response.json()
data
```

## Income statement 


```python
import requests

response = requests.get('https://www.alphavantage.co/query?function=INCOME_STATEMENT&symbol=IBM&apikey=demo')
data = response.json()
data
```

## Balance sheet 


```python
import requests

response = requests.get('https://www.alphavantage.co/query?function=BALANCE_SHEET&symbol=IBM&apikey=demo')

data = response.json()
data
```

## Cashflow statement


```python
import requests

response = requests.get('https://www.alphavantage.co/query?function=CASH_FLOW&symbol=IBM&apikey=demo')

data = response.json()
data
```
