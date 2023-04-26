<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stripe/Stripe_List_all_customers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Stripe+-+List+all+customers:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #stripe #api #customers #list #python #reference

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook will list all customers from Stripe and explain how to use the Stripe API to do so. It is usefull for organizations that need to manage their customers.

**References:**
- [Stripe API Documentation](https://stripe.com/docs/api/customers/list)
- [Stripe Python Library](https://stripe.com/docs/stripe-python)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [API key](https://stripe.com/docs/keys) used to authenticate with Stripe


```python
api_key = naas.secret.get("STRIPE_API_KEY", ) or "sk_test_4eC39HqLyjWDarjtT1zdp7dc"
```

## Model

### List all customers


```python
# URL
stripe_endpoint = "https://api.stripe.com/v1/customers"

# Define headers with authorization using Stripe API key
headers = {
    "Authorization": f"Bearer {api_key}"
}

# Send GET request to Stripe API to list customers
response = requests.get(stripe_endpoint, headers=headers)

# Check for successful response (status code 200)
if response.status_code == 200:
    # Get the customers from the response
    customers = response.json()["data"]
    
    # Check if there are more customers to fetch
    while response.json()["has_more"]:
        # Set the starting_after parameter to the last customer ID from the previous response
        starting_after = customers[-1]["id"]
        
        # Send GET request with the starting_after parameter to fetch the next set of customers
        response = requests.get(stripe_endpoint, headers=headers, params={"starting_after": starting_after})
        
        # Check for successful response (status code 200)
        if response.status_code == 200:
            # Get the customers from the response
            customers.append(response.json()["data"])
```

## Output

### Display result


```python
print("Customer fetched:", len(customers))
pprint(customers[0])
```
