<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Update_a_Bitlink.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Update+a+Bitlink:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #update #bitlink #reference #dev

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to update fields in the specified link using Bitly API.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#updateBitlink)
- [Bitly API Documentation](https://dev.bitly.com/v4/#operation/updateBitlink)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `token`: [Generate a Bitly Access Token](https://dev.bitly.com/get_started/#step-1-generate-an-access-token)
- `bitlink`: Bitlink to be updated
- `title`: New title for the Bitlink
- `long_url`: New long URL for the Bitlink


```python
token = "<YOUR_TOKEN_HERE>"
bitlink = "<YOUR_BITLINK_HERE>"
title = "<YOUR_TITLE_HERE>"
long_url = "<YOUR_LONG_URL_HERE>"
```

## Model

### Update Bitlink

Update fields in the specified link.


```python
url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}"
headers = {"Authorization": f"Bearer {token}"}
data = {"title": title, "long_url": long_url}
response = requests.patch(url, headers=headers, json=data)
```

## Output

### Display result


```python
response.json()
```

 
