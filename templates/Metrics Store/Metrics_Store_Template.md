<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Metrics%20Store/Metrics_Store_Template.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #tag1 #tag2

## Input

### Import library


```python
import naas_drivers
```

### Variables


```python
stock_name = 'NFLX'  
```

## Model

### Function


```python
table = naas_drivers.yahoofinance.get(stock_name, date_from=-3600, date_to="today", moving_averages=[20,50])
```

## Output

### Display result


```python
table
```
