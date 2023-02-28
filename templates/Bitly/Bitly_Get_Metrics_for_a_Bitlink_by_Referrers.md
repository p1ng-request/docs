<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_Metrics_for_a_Bitlink_by_Referrers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+Metrics+for+a+Bitlink+by+Referrers:+Error+short+description">Bug report</a>

**Tags:** #bitly #api #metrics #bitlink #referrers #dev

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to use the Bitly API to get metrics for a Bitlink by Referrers.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getMetricsForBitlinkByReferrers)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
from pprint import pprint
import naas
```

### Setup Variables
- **access_token**: Access token for authentication. [Get your access token](https://dev.bitly.com/authentication.html).
- **bitlink**: Bitlink for which you want to get metrics.


```python
access_token = naas.secret.get("BITLY_TOKEN") or "<YOUR_TOKEN_HERE>"
bitlink = "bit.ly/3lU6hRt"
```

## Model

### Get Metrics for a Bitlink by Referrers

This function will return referrer click counts for the specified link.


```python
def get_metrics_for_bitlink_by_referrers(access_token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/referrers"
    headers = {"Authorization": f"Bearer {access_token}"}
    res = requests.get(url, headers=headers)
    return res.json()
```

## Output

### Display result


```python
result = get_metrics_for_bitlink_by_referrers(access_token, bitlink)
pprint(result)
```

 
