<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/CCXT/CCXT_Predict_Bitcoin_from_Binance.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #ccxt #bitcoin #trading

## Input

### Install package


```python
pip install ccxt --user
```

### Import libraries


```python
import naas
import ccxt
import pandas as pd
from datetime import datetime
from naas_drivers import plotly, prediction
```

## Model

### Recovery of the api secret keys


```python
binance = ccxt.binance({
    'apiKey': naas.secret.get('binance_api'),
    'secret': naas.secret.get('binance_secret')
}) 
# binance['api'] = binance['test']

data = binance.fetch_ohlcv(symbol = 'BTC/USDT', limit = 200, timeframe = '1d')
```

### Mapping of the candlestick plot


```python
df = pd.DataFrame(data, columns=["Date","Open","High","Low","Close","Volume"])
df['Date'] = [datetime.fromtimestamp(float(time)/1000) for time in df['Date']]
```

### Attribute the candlesticks variables


```python
chart_candlestick = plotly.candlestick(df,
    label_x="Date", 
    label_open="Open", 
    label_high="High",
    label_low="Low",
    label_close="Close"
)
```


```python
df[f"MA{20}"] = df.Close.rolling(
                    20
                ).mean()
df[f"MA{50}"] = df.Close.rolling(
                    50
                ).mean()
```

### Get the prediction for the stock plot


```python
pr = prediction.get(dataset=df)
chart_stock = plotly.stock(pr, kind="linechart"
)
```

## Output

### Display bitcoin plot prediction by changing resolution


```python
chart_stock.update_layout(
    autosize=True,
    width=1300,
    height=800,
)
```
