<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Naas - Get Transactions
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Get_Transactions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #credits

## Input

### Import library


```python
from naas_drivers import naascredits
import pandas as pd
```

### Variables


```python
page_size = "100000"
```

## Model

### Function


```python
df = pd.DataFrame(naascredits.connect().transactions.get(page_size=page_size))
df
```

## Output

### Display result


```python
df.to_csv('billing.csv')
```
