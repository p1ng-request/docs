<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Metrics_for_a_Bitlink_by_Country.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Metrics+for+a+Bitlink+by+Country:+Error+short+description">Bug report</a>

**Tags:** #bitly #api #metrics #bitlink #country #reference

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use the Bitly API to get metrics for a Bitlink by Country.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getMetricsForBitlinkByCountries)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
import naas
import json
```

### Setup Variables
- **access_token**: [Generate an access token](https://dev.bitly.com/authentication.html)
- **bitlink**: The Bitlink for which you want to get metrics


```python
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN>"
bitlink = "bit.ly/3lU6hRt"
```

## Model

### Get Metrics for a Bitlink by Country

This function will use the Bitly API to get metrics for a Bitlink by Country.


```python
def get_metrics_by_country(access_token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/countries"
    headers = {"Authorization": f"Bearer {access_token}"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return json.loads(response.content)
    else:
        return None
```

## Output

### Display result


```python
metrics_by_country = get_metrics_by_country(access_token, bitlink)
if metrics_by_country:
    print(json.dumps(metrics_by_country, indent=4))
else:
    print("An error occurred.")
```

 
