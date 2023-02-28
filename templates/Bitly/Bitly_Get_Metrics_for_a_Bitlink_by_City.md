<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Metrics_for_a_Bitlink_by_City.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Metrics+for+a+Bitlink+by+City:+Error+short+description">Bug report</a>

**Tags:** #bitly #api #metrics #city #bitlink #dev

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will return the city origins of click traffic for the specified link. This feature is only available for paid account.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getMetricsForBitlinkByCities)
- [Bitly Documentation](https://dev.bitly.com/v4/#operation/getMetricsForBitlinkByCities)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
- `access_token`: Bitly access token. [Get your token here](https://dev.bitly.com/authentication.html).
- `bitlink`: Bitlink to get clicks by city.


```python
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN>"
bitlink = "bit.ly/3lU6hRt"
```

## Model

### Get Metrics for a Bitlink by City

This function will return the city origins of click traffic for the specified link.


```python
def get_metrics_by_city(bitlink, access_token):
    url = "https://api-ssl.bitly.com/v4/bitlinks/{}/cities".format(bitlink)
    headers = {"Authorization": "Bearer {}".format(access_token)}
    response = requests.get(url, headers=headers)
    return response.json()
```

## Output

### Display result


```python
metrics_by_city = get_metrics_by_city(bitlink, access_token)
pprint(metrics_by_city)
```

 
