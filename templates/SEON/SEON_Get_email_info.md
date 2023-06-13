<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/SEON/SEON_Get_email_info.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=SEON+-+Get+email+info:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #seon #email #enrichment #api #tool #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use SEON's standalone email enrichment tool to learn about the approximate minimum age of an email address, its provider, and any connected online profiles and save it into a json file.

*Good to know:*
- You can use the Fraud API if you want to use the Email API together with any of our  Phone API, IP API, and Device Fingerprinting.
- All SEON API requests are case-sensitive. Please follow the formatting below to avoid errors.
- Email API requests are limited to 120/minute during your SEON free trial.

**References:**
- [SEON API Reference](https://docs.seon.io/api-reference#email-api)
- [SEON Documentation](https://docs.seon.io/getting-started)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
import json
```

### Setup Variables
[Get your SEON license_key](https://admin.seon.io/my-account/#profile)
- `license_key`: SEON license key 
- `email`: Email address to be enriched


```python
# Inputs
license_key = naas.secret.get("SEON_LICENSE_KEY") or "YOUR_LICENSE_KEY"
email = "florent.ravenel1@gmail.com"

# Outputs
output_json = f"SEON_{email}_info.json"
```

## Model

### Get email info
[Enrichment and Scoring](https://docs.seon.io/api-reference#step-2-enrichment-and-scoring)


```python
def get_email_info(license_key, email):
    headers = {
        "X-API-KEY": license_key
    }
    req_url = f"https://api.seon.io/SeonRestService/email-api/v2.2/{email}"
    res = requests.get(req_url, headers=headers)
    res.raise_for_status
    return res.json()

email_info = get_email_info(license_key, email)
print(f"✅ Email '{email}' score:", email_info.get("data").get("score"))
pprint(email_info)
```

## Output

### Save json file

Using the `json.dump()` function, the `data` dictionary can be saved to a json file.


```python
with open(output_json, "w") as f:
    json.dump(email_info, f)
```

 
