<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Transform_dataframe_to_dict.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #pandas #dict #snippet #yahoofinance #naas_drivers 

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

With this template, you can convert dataframe to dictionary in pandas WITHOUT index

## Input

### Import libraries


```python
from naas_drivers import yahoofinance
```

### Input parameters
👉 Here you can change the ticker, timeframe and add moving averages analysis


```python
ticker = "TSLA"
date_from = -100
date_to = 'today'
```

## Model

### Get dataframe from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker,
                            date_from=-5)
df_yahoo
```

## Output

### Transform dataframe
Params = orient
- list: keys are column names, values are lists of column data
- records: each row becomes a dictionary where key is column name and value is the data in the cell


```python
dict_yahoo = df_yahoo.to_dict(orient="records")
dict_yahoo
```
