<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Abstract%20API/Abstract_API_Check_Email_Validation.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Abstract+API+-+Check+Email+Validation:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #abstractapi #email #validation #api #check #tester

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use Abstract API to check if an email is valid.

**References:**
- [Abstract API - Email Validation](https://app.abstractapi.com/api/email-validation/tester)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [Get your API key](https://app.abstractapi.com/signup)
- `email`: Email to be validated


```python
api_key = naas.secret.get("ABSTRACT_API") or "YOUR_API_KEY"
email = "florent@naas.ai"
```

## Model

### Validate Email

Validate an email address using Abstract API's Email Validation API.


```python
url = f"https://emailvalidation.abstractapi.com/v1/?api_key={api_key}&email={email}"
response = requests.get(url)
```

## Output

### Display result


```python
pprint(response.json())
```

 
