<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Metrics_for_a_Bitlink_by_Devices.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Metrics+for+a+Bitlink+by+Devices:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #metrics #devices

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to use the Bitly API to get metrics for a Bitlink by devices. This endpoint is only available for paid account.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getMetricsForBitlinkByDevices)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
from pprint import pprint
import naas
```

### Setup Variables
- **access_token**: [Bitly Authentication](https://dev.bitly.com/authentication.html)
- **bitlink**: Bitlink to get metrics for


```python
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN_HERE>"
bitlink = "bit.ly/3lU6hRt"
```

## Model

### Get Metrics for a Bitlink by Device Type

This function will use the Bitly API to get metrics for a Bitlink by device type.


```python
def get_metrics_by_device_type(access_token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/devices/"
    headers = {"Authorization": f"Bearer {access_token}"}
    res = requests.get(url, headers=headers)
    return res.json()
```

## Output

### Display result


```python
result = get_metrics_by_device_type(access_token, bitlink)
pprint(result)
```

 
