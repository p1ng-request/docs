<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Request/Request_Handling_Errors_and_Exceptions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Request+-+Handling+Errors+and+Exceptions:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #request #error #exception #handling #python #library

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook template explores how to handle errors and exceptions when using the requests library. It provides examples of error handling techniques, including proper status code checking, handling timeouts, and dealing with connection errors.

**References:**
- [Requests Documentation](https://requests.readthedocs.io/en/master/)
- [Python Exceptions](https://docs.python.org/3/tutorial/errors.html)
- [Status Code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

## Input

### Import libraries


```python
import requests
```

### Setup Variables
- `url`: URL of the API endpoint
- `timeout`: Timeout in seconds for the request
- `response`: Response to the requests. Usually in data


```python
url = "https://api.example.com/endpoint"
timeout = 100
response = None
```

## Model

### Making a Request


```python
try:
    response = requests.get(url, timeout=timeout)
    response.raise_for_status()  # Raises an exception if the response status code is not 2xx
    data = response.json()
    # Process the data
    print("Data retrieved successfully:", data)
except requests.exceptions.RequestException as e:
    # Handle connection errors, timeouts, and other request exceptions
    print("Error occurred:", e)
except requests.exceptions.HTTPError as e:
    # Handle HTTP errors (status codes 4xx and 5xx)
    print("HTTP Error occurred:", e)
except ValueError as e:
    # Handle JSON decoding errors
    print("JSON decoding error occurred:", e)
except Exception as e:
    # Handle any other unexpected exceptions
    print("An unexpected error occurred:", e)
```

## Output

### Display result


```python
# Display the response
print(response)
```

 
