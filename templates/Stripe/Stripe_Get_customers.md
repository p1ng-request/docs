<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_Get_customers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Stripe+-+Get+customers:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #stripe #customers #snippet #operations #dataframe

**Author:** [Martin Donadieu](https://www.linkedin.com/in/martindonadieu/)

**Description:** This notebook provides a guide to acquiring customers through Stripe.

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
pd.DataFrame(customers.get("data"))
```
