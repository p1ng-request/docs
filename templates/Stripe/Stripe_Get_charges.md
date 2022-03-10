<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_Get_charges.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #stripe #charges #snippet

**Author:** [Martin Donadieu](https://www.linkedin.com/in/martindonadieu/)

## Input

### Import libraries


```python
try:
    import stripe
except:
    !pip install stripe
    import stripe
import pandas as pd
```


```python
api_key = "sk_test_4eC39HqLyjWDarjtT1zdp7dc"
```

## Model

### Connect to the API


```python
stripe.api_key = api_key
```


```python
charges = stripe.Charge.list(limit=30)
```

## Output

### Display result


```python
pd.DataFrame(charges.get('data'))
```
