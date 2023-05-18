<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_Retrieve_a_customer.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Stripe+-+Retrieve+a+customer:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #stripe #payment #customer #api #python #retrieve #crud

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to retrieve a customer using the Stripe API. It is usefull for organizations that need to manage customer payments.

**References:**
- [Stripe API Documentation](https://stripe.com/docs/api/customers/retrieve?lang=python)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [API key](https://stripe.com/docs/keys) used to authenticate with Stripe
- `customer_id`: Customer ID to be retrieved


```python
api_key = naas.secret.get("STRIPE_API_KEY_TEST") or "sk_test_4eC39HqLyjWDarjtT1zdp7dc"
customer_id = "cus_NurehC5tkWOv38"
```

## Model

### Retrieve a customer


```python
def get_customer(api_key, object_id):
    # Init
    stripe_endpoint = f"https://api.stripe.com/v1/customers/{object_id}"

    # Define headers with authorization using Stripe API key
    headers = {
        "Authorization": f"Bearer {api_key}"
    }

    # Send DELETE request to Stripe API to delete a customer
    response = requests.get(stripe_endpoint, headers=headers)
    return response
```

## Output

### Display result


```python
response = get_customer(api_key, customer_id)
if response.status_code == 200:
    print(f"✅ Customer successfully retrieved")
else:
    print(f"❌ Error retrieving the customer")
response.json()
```

 
