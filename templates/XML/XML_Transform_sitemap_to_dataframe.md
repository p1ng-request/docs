<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# XML - Transform sitemap to dataframe
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/XML/XML_Transform_sitemap_to_dataframe.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #xml #file #tool

## Install needed library


```python
pip install xmltodict
```

## Run the magic code


```python
import json 
import xmltodict
import pandas as pd
import requests

def sitemap_to_df(url):
    df = None
    key = "urlset.url.url"
    r = requests.get(f'{url}/sitemap.xml')
    data_dict = xmltodict.parse(r.content) 
    if key and len(key.split('.')) > 0:
        keys = key.split('.')
        keys.reverse()
        data = data_dict.get(keys.pop())
        while(len(keys) > 1):
            data = data.get(keys.pop())
        df = pd.DataFrame.from_dict(data=data)
    elif key and data_dict.get(key):
        df = pd.DataFrame.from_dict(data=data_dict.get(key))
    else:
        df = pd.DataFrame.from_dict(data=data_dict)
    return df

```

## Input

### Import library


```python
import naas
```

### Choose the website you want


```python
website = "https://zapier.com"
```

## Model

### Get your Dataframe


```python
df = sitemap_to_df(website)
df
```

## Output

### Set the timezone


```python
naas.get_remote_timezone()
```


```python
naas.set_remote_timezone("Europe/Lisbon")
```
