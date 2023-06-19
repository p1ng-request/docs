<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Request/Request_Sending_POST_Requests_with_Data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Request+-+Sending+POST+s+with+Data:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #requests #post #data #python #library #api

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook template demonstrates how to use the requests library to send a POST request with data. It includes importing the library, preparing the data, making the request, handling the response, and verifying the successful submission.

**References:**
- [Python Requests post() Method](https://www.w3schools.com/python/ref_requests_post.asp)
- [HTTP POST Request](https://www.w3schools.com/tags/ref_httpmethods.asp)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `url`: URL of the endpoint to send the POST request
- `data`: Optional. A dictionary, list of tuples, bytes or a file object to send to the specified url
- `json`: Optional. A JSON object to send to the specified url
- `headers`: Optional. A JSON object to send to the specified url
- `cookies`: Optional. A dictionary of cookies to send to the specified url.

In the context of a POST request, the "data" parameter refers to the payload or body of the request, which can be any type of data (such as text, binary, or JSON). The "JSON parameters" refer to specific key-value pairs within the data payload that are formatted as JSON objects, allowing for structured data representation and easy parsing on the server side. JSON parameters are a subset of the overall data being sent in the POST request.


```python
url = "https://www.example.com/endpoint"
json = {
    'key1': 'value1',
    'key2': 'value2',
    # Add more key-value pairs as needed
}
data = {}
headers = {}
cookies = {}
```

## Model

### Send POST Request

The `requests.post()`function sends a POST request to the specified `url` with the supplied `data`. It retrieves the response from the server and assigns it to the `response` variable. The response contains details such as status code, headers and content. It is crucial to handle the response correctly, taking into account the status code to determine the success or failure of the request.


```python
response = requests.post(
    url,
    data=data,
    json=json,
    headers=headers,
    cookies=cookies
)
```

## Output

### Display result


```python
# Handle the response
if response.status_code == 200:
    # Successful request
    print('Request was successful')
    print(response.text)  # Print the response content
else:
    # Request was not successful
    print('Request failed')
    print('Status code:', response.status_code)
    print('Error message:', response.text)
```
