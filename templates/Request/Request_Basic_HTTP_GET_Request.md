<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Request/Request_Basic_HTTP_GET_Request.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Request+-+Basic+HTTP+GET:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #request #http #get #library #python #api

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook provides a template for making a basic HTTP GET request using the requests library. It covers importing the library, making the request, handling the response, and displaying the retrieved data.

**References:**
- [Requests: HTTP for Humans](https://requests.readthedocs.io/en/master/)
- [HTTP GET Request](https://www.w3schools.com/tags/ref_httpmethods.asp)
- [Status Codes Response](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `url`: URL of the API endpoint


```python
url = "https://api.chucknorris.io/jokes/random"
```

## Model

### Make HTTP GET Request

The `requests.get()` function performs all the necessary behind-the-scenes operations to establish the connection with the server, send the request, and handle the response. It abstracts away the complexities of dealing with low-level network protocols and provides a simplified interface for making HTTP requests.


```python
# Make the request
response = requests.get(url)
```

## Output

### Display result


```python
if response.status_code == 200:
        # Display the response headers
    print("Response Headers:")
    for header, value in response.headers.items():
        print(f"{header}: {value}")
    print()
    
    # Retrieve the data from the response
    data = response.json()
    # Display the retrieved data
    print("Response Data:")
    print(data)
else: 
    # If the request was not successful, print the status code
    print('Request failed with status code:', response.status_code)
```

 
