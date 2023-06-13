<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Bitly/Bitly_Delete_a_Bitlink.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Bitly+-+Delete+a+Bitlink:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #bitly #api #delete #bitlink #hash #unedited

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to delete an unedited hash Bitlink.

**References:**
- [Bitly API Reference](https://dev.bitly.com/api-reference/#deleteBitlink)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `token`: [Generate a Bitly Access Token](https://dev.bitly.com/get_started.html#step-2-generate-an-access-token)
- `bitlink`: unedited hash Bitlink to delete


```python
token = "<YOUR_TOKEN_HERE>"
bitlink = "<YOUR_BITLINK_HERE>"
```

## Model

### Delete Bitlink

This function will delete an unedited hash Bitlink.


```python
def delete_bitlink(token, bitlink):
    url = f"https://api-ssl.bitly.com/v4/bitlinks/{bitlink}"
    headers = {"Authorization": f"Bearer {token}"}
    response = requests.delete(url, headers=headers)
    return response
```

## Output

### Display result


```python
response = delete_bitlink(token, bitlink)
print(response.status_code)
print(response.json())
```

 
