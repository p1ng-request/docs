<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Quandl/Quandl_Get_data_from_CSV.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Quandl+-+Get+data+from+CSV:+Error+short+description">Bug report</a>

**Tags:** #quandl #marketdata #opendata #finance #snippet #csv

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook provides a guide to retrieving data from CSV files using the Quandl API.

## Input

### Import librairies


```python
import matplotlib.pyplot as plt
import pandas as pd
import os
```

## Model

### Read CSV with pandas


```python
data = pd.read_csv(
    "https://www.quandl.com/api/v3/datasets/BITFINEX/BTCUSD.csv?api_key=bxrSXWimkiknuCcV71uL"
)
data
```

## Output

### Visualize & plot chart


```python
%matplotlib inline
```


```python
data.plot()
```
