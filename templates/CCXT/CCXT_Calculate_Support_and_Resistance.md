<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# CCXT - Calculate Support and Resistance
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/CCXT/CCXT_Calculate_Support_and_Resistance.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #ccxt #bitcoin #trading

Prerequisite : get binance API Key


```python
!pip install trendln matplotlib==3.1.3 --user
```


```python
import naas
import ccxt
import pandas as pd
from datetime import datetime
import naas_drivers
import trendln
```


```python
binance = ccxt.binance({
    'apiKey': naas.secret.get('binance_api'),
    'secret': naas.secret.get('binance_secret')
}) 
data = binance.fetch_ohlcv(symbol = 'BTC/USDT', limit = 180, timeframe = '4h')
```


```python
df = pd.DataFrame(data, columns=["Date","Open","High","Low","Close","Volume"])
df['Date'] = [datetime.fromtimestamp(float(time)/1000) for time in df['Date']]
df
```


```python
fig = trendln.plot_support_resistance(
    df[-1000:].Close, #as per h for calc_support_resistance
    xformatter = None, #x-axis data formatter turning numeric indexes to display output
      # e.g. ticker.FuncFormatter(func) otherwise just display numeric indexes
    numbest = 1, #number of best support and best resistance lines to display
    fromwindows = True, #draw numbest best from each window, otherwise draw numbest across whole range
    pctbound = 0.1, # bound trend line based on this maximum percentage of the data range above the high or below the low
    extmethod = trendln.METHOD_NUMDIFF,
    method=trendln.METHOD_PROBHOUGH,
    window=125,
    errpct = 0.005,
    hough_prob_iter=50,
    sortError=False,
    accuracy=1)
```


```python
import plotly.tools as tls
import plotly.graph_objects as go

plotly_fig = tls.mpl_to_plotly(fig)
```


```python
layout = dict(
    dragmode="pan",
    xaxis_rangeslider_visible=False,
    showlegend=True,
)
new_data = list(plotly_fig.data)
new_data.pop(2)
new_data.pop(2)
new_data.pop(1)
new_data.pop(1)
fig = go.Figure(data=new_data, layout=layout)
fig
```


```python

```
