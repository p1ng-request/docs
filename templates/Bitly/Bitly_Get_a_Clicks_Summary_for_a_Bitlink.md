    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Get_a_Clicks_Summary_for_a_Bitlink.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Get+a+Clicks+Summary+for+a+Bitlink:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #clicks #summary #bitlink #reference

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get a Clicks Summary for a Bitlink using the Bitly API.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#getClicksSummaryForBitlink)
- [Bitly Authentication](https://dev.bitly.com/authentication.html)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `token`: [Bitly Authentication](https://dev.bitly.com/authentication.html)
- `bitlink`: Bitlink to get the Clicks Summary


```python
token = "<YOUR_TOKEN>"
bitlink = "<YOUR_BITLINK>"
```

## Model

### Get Clicks Summary for a Bitlink

This function will get a Clicks Summary for a Bitlink using the Bitly API.


```python
def get_clicks_summary_for_bitlink(token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}/clicks/summary"
    headers = {"Authorization": f"Bearer {token}"}
    response = requests.get(url, headers=headers)
    return response.json()
```

## Output

### Display result


```python
clicks_summary = get_clicks_summary_for_bitlink(token, bitlink)
clicks_summary
```

 
