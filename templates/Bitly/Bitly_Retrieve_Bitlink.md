<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Retrieve_Bitlink.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Retrieve+Bitlink:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #list #active #links #python #bitlink

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will return information for a specified bitlink using the Bitly API.

<u>References:</u>
- [Bitly API Documentation](https://dev.bitly.com/v4_documentation.html)
- [Bitly API Quickstart](https://dev.bitly.com/v4/#section/Quick-Start)

## Input

### Import libraries


```python
import requests
import json
import naas
from pprint import pprint
```

### Setup Variables
- **token**: [Generate a Bitly Access Token](https://support.bitly.com/hc/en-us/articles/230647907-How-do-I-generate-an-OAuth-access-token-for-the-Bitly-API-)
- **bitlink**: A Bitlink made of the domain and hash 


```python
token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN_HERE>"
bitlink = "bit.ly/3lU6xxxt"
```

## Model

### Retrieve a Bitlink


```python
def retrieve_bitlink(token, bitlink):
    headers = {"Authorization": f"Bearer {token}"}
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}"
    response = requests.get(url, headers=headers)
    response.raise_for_status()
    return response.json()

link = retrieve_bitlink(token, bitlink)
```

## Output

### Display result


```python
pprint(link)
```

 
