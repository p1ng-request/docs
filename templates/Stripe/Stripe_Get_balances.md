<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Stripe - Get balances
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_Get_balances.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #stripe #balances

## Input

### Install packages


```python
!pip install stripe
```

### Import library


```python
import stripe
import pandas as pd
```

### Variables


```python
api_key = "sk_test_4eC39HqLyjWDarjtT1zdp7dc"
```

## Model

### Connect to the API


```python
stripe.api_key = api_key
```


```python
balance = stripe.BalanceTransaction.list(limit=30)
```

## Output

### Get the balance


```python
pd.DataFrame(balance.get('data'))
```
