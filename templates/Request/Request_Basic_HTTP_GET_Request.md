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

    Response Headers:
    Date: Wed, 14 Jun 2023 09:52:03 GMT
    Content-Type: application/json;charset=UTF-8
    Transfer-Encoding: chunked
    Connection: keep-alive
    Via: 1.1 vegur
    CF-Cache-Status: DYNAMIC
    Report-To: {"endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report\/v3?s=AeEt8OHIGV4JscmRKR85feoGQ9DWj3NWvAenVpLJ%2B6TdOLs6jq7XKWzoopCZJrPVzQmXtMAbVjFSCm%2F3pYNC7GFL106GldQNrheIDEKbu%2BKqyct5jwR%2FR8ZlFH6H%2B0zaNkmqhac%3D"}],"group":"cf-nel","max_age":604800}
    NEL: {"success_fraction":0,"report_to":"cf-nel","max_age":604800}
    Server: cloudflare
    CF-RAY: 7d71ada52d4603f5-CDG
    Content-Encoding: br
    alt-svc: h3=":443"; ma=86400
    
    Response Data:
    {'categories': [], 'created_at': '2020-01-05 13:42:24.696555', 'icon_url': 'https://assets.chucknorris.host/img/avatar/chuck-norris.png', 'id': 'wGbqgcxRQumTYd6y55cHwA', 'updated_at': '2020-01-05 13:42:24.696555', 'url': 'https://api.chucknorris.io/jokes/wGbqgcxRQumTYd6y55cHwA', 'value': "Chuck Norris ripped the horn off of the world's last unicorn. He made a scrimshawed knife handle out of it."}


 
