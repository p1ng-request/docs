<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/ZeroBounce/ZeroBounce_Validate_Single_Email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=ZeroBounce+-+Validate+Single+Email:+Error+short+description">Bug report</a>

**Tags:** #zerobounce #email #validation #java #sdk #setup

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to validate a single email address using ZeroBounce API.

**References:**
- [Complete API Libraries and Wrappers](https://www.zerobounce.net/docs/zerobounce-api-wrappers/#api_wrappers__v2__python)
- [ZeroBounce Email Validation](https://www.zerobounce.net/docs/email-validation-api-quickstart)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `api_key`: [Get your API key](https://www.zerobounce.net/members/API)
- `email`: email to be validated
- `ip_address`: ip_address can be blank


```python
api_key = naas.secret.get("ZEROBOUNCE_API_KEY") or "YOUR_API_KEY"
email = "florent@naas.ai"
ip_address = ""
```

## Model

### Validate single email


```python
url = "https://api.zerobounce.net/v2/validate"
params = {
    "email": email,
    "api_key": api_key,
    "ip_address": ip_address
}
response = requests.get(url, params=params)
print("Email status:", response.json().get("status"))
```

## Output

### Print the returned json


```python
pprint(response.json())
```
