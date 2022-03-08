<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_Get_customers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #stripe #customers

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

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
customers = stripe.Customer.list(limit=30)
```

## Output

### Get customers


```python
pd.DataFrame(customers.get('data'))
```
