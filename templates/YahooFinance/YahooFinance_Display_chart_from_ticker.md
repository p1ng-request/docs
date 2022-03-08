With this template, you can get data from any ticker available in [Yahoo finance](https://finance.yahoo.com/quote/TSLA/).<br> 

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import libraries


```python
from naas_drivers import yahoofinance, plotly
```

### Input parameters
👉 Here you can change the ticker, timeframe and add moving averages analysiss


```python
ticker = "TSLA"
date_from = -365
date_to = "today"
interval = '1d'
moving_averages = [20, 50]
```

## Model

### Get dataset from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker,
                            date_from=date_from,
                            date_to=date_to,
                            interval=interval,
                            moving_averages=moving_averages)
```

## Output

### Display chart


```python
chart = plotly.linechart(df_yahoo,
                         x="Date",
                         y=["Close", "MA20", "MA50"],
                         showlegend=True,
                         title=f"{ticker} stock as of today")
```
