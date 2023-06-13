<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Clicks_for_a_Bitlink.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Clicks+for+a+Bitlink:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #getclicks #bitlink #python #dev

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to use the Bitly API to get the click counts for a specified link in an array based on a date.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getClicksForBitlink)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
import naas
import json
```

### Setup Variables
- `access_token`: Bitly access token. [Get your token here](https://dev.bitly.com/authentication.html).
- `bitlink`: Bitlink to get clicks for.
- `unit`: Unit of time for the response.
- `units`: Number of units of time to query data for.


```python
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN>"
bitlink = "bit.ly/3lU6hRt"
unit = "day"
units = -1
```

## Model

### Get Clicks for a Bitlink

This function will use the Bitly API to get the click counts for the specified link in an array based on a date.


```python
def get_clicks_for_bitlink(token, bitlink, unit, units):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/clicks"
    headers = {"Authorization": f"Bearer {token}"}
    params = {"unit": unit, "units": units}
    response = requests.get(url, headers=headers, params=params)
    response.raise_for_status()
    return response.json()
```

## Output

### Display result


```python
clicks = get_clicks_for_bitlink(access_token, bitlink, unit, units)
print(json.dumps(clicks, indent=4))
```

 
