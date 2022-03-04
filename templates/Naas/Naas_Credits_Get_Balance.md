<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Naas - Credits Get Balance
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Credits_Get_Balance.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #credits

## Input

### Import library


```python
from naas_drivers import naascredits
```

## Model

### Function


```python
balance = naascredits.connect().get_balance()
```

## Output

### Display result


```python
balance
```
