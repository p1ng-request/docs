<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Create_Links.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Create+Links:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #link #shorten #url #create #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to create short links with Bitly.

<u>References:</u>
- [Bitly Documentation](https://dev.bitly.com/v4_documentation.html)
- [Bitly API](https://dev.bitly.com/get_started.html)

## Input

### Import libraries


```python
import requests
import json
```

### Setup Variables
- `token`: [Generate a Bitly Access Token](https://dev.bitly.com/get_started.html)
- `long_url`: URL to be shortened


```python
token = "<YOUR_TOKEN_HERE>"
long_url = "https://www.example.com/"
```

## Model

### Shorten URL

This function will use the Bitly API to shorten a given URL.


```python
def shorten_url(token, long_url):
    url = "https://api-ssl.bitly.com/v4/shorten"
    headers = {"Authorization": "Bearer " + token}
    payload = {"long_url": long_url}
    response = requests.post(url, headers=headers, json=payload)
    response_json = response.json()
    return response_json["link"]
```

## Output

### Display result


```python
short_url = shorten_url(token, long_url)
print(short_url)
```

 
