    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Creditsafe/Creditsafe_Get_Company_Credit_Report.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Creditsafe+-+Get+Company+Credit+Report:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #creditsafe #api #enterprise #integrations #company #creditreport

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use the Creditsafe API to get a company credit report.

**References:**
- [Creditsafe Free Trial](https://www.creditsafe.com/gb/en/forms/free-trial.html?cta=Free%20trial&previousPage=api-documentation)
- [Creditsafe API Documentation](https://www.creditsafe.com/gb/en/enterprise/integrations/api-documentation.html#tag/Companies/operation/companyCreditReport)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
import json
```

### Setup Variables
- `username`: username used to connect to Creditsafe
- `password`: password used to connect to Creditsafe
- `env`: if 'sandbox' then we will change BASE URL
- `company_id`: company ID used in Creditsafe
- `siret`: SIRET to be set (if French company)


```python
# Inputs
username = naas.secret.get("CREDITSAFE_USERNAME")
password = naas.secret.get("CREDITSAFE_PASSWORD")
env = "sandbox"
company_id = None
siret = "85272297400056"

# Outputs
json_path = 'creditsafe_company_report.json'
```

## Model

### Create base url


```python
if env == "sandbox":
    BASE_URL = f"https://connect.sandbox.creditsafe.com/v1"
else:
    BASE_URL = "https://connect.creditsafe.com/v1"    
```

### Get access token


```python
def get_access_token(
    username,
    password
):
    # Init
    url = f"{BASE_URL}/authenticate"
    
    # Headers
    headers = {
        "Content type": "application/json"
    }
    
    # Payload
    data = {
        "username": username,
        "password": password,
    }
    
    # Request
    res = requests.post(url, headers=headers, data=data)
    res.raise_for_status
    if res.status_code == 200:
        return res.json().get("token")
    else:
        return None
    
access_token = get_access_token(username, password)
```

### Get Company Credit Report


```python
def get_company_report(
    access_token,
    company_id=None,
    siret=None
):
    # Init
    company_report = None
    if siret:
        company_id = f'FR-X-{siret}'
    if company_id:
        url = f"{BASE_URL}/companies/{company_id}?language=fr"
        
        # Headers
        headers = {
            "Authorization": f"Bearer {access_token}"
        }

        # Request
        res = requests.get(url, headers=headers)
        res.raise_for_status
        if res.status_code == 200:
            company_report = res.json()
    return company_report, company_id
    
company_report, company_id = get_company_report(
    access_token,
    company_id=company_id,
    siret=siret
)
```

## Output

### Display result


```python
if company_report:
    # Display summary
    print("✅ Company summary:")
    pprint(company_report.get("report").get("companySummary"))
    
    # Save json
    if json_path == 'creditsafe_company_report.json':
        json_path = f'creditsafe_company_report_{company_id}.json'
    with open(json_path, 'w') as outfile:
        json.dump(company_report, outfile)
    print("✅ Json saved:", json_path)
```
