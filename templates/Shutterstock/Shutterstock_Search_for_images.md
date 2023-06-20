<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Shutterstock/Shutterstock_Search_for_images.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Shutterstock+-+Search+for+images:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #shutterstock #images #search #api #reference #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to use the Shutterstock API to search for images.

**References:**
- [Shutterstock API Reference](https://api-reference.shutterstock.com/#images)

## Input

### Import libraries


```python
import json
import naas
import requests
from PIL import Image
import io
import matplotlib.pyplot as plt
import pydash
```

### Setup Variables
- `api_key`: [Get your API key](https://developers.shutterstock.com/getting-started)
- `query`: The search query


```python
api_key = naas.secret.get("SHUTTERSTOCK_KEY")
query = "cat"
```

## Model

### Search for images

This function will search for images using the Shutterstock API.


```python
def search_images(api_key, query):
    url = "https://api.shutterstock.com/v2/images/search"
    params = {
        "query": query,
        "view": "minimal",
        "sort": "popular",
        "page": 1,
        "per_page": 10,
    }
    headers = {"Authorization": "Bearer " + api_key}
    response = requests.get(url, params=params, headers=headers)
    return response.json()

result = search_images(api_key, query)
print("Total result", result.get("total_count"))
```

## Output

### Display result


```python
def display_image_from_url(image_url):
    # Download the image from the URL
    response = requests.get(image_url)
    image_bytes = response.content

    # Open the image from bytes
    image = Image.open(io.BytesIO(image_bytes))

    # Display the image
    plt.imshow(image)
    plt.axis('off')
    plt.show()
    
for d in result.get("data"):
    image_url = pydash.get(d, "assets.preview.url")
    print("Image URL:", image_url)
    display_image_from_url(image_url)
```

 
