<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WAQI/WAQI_Search_station_by_name.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WAQI+-+Search+station+by+name:+Error+short+description">Bug report</a>

**Tags:** #waqi #airquality #api #data #city #python #stations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to search stations by name using AQI API.

**References:**
- [WAQI API Documentation](https://aqicn.org/json-api/doc/#api-Search-SearchByName)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Variables
- `token`: WAQI API token. [Get your token here](https://aqicn.org/data-platform/token/).
- `keyword`: Keyword to find station.


```python
token = naas.secret.get("WAQI_TOKEN") or "YOUR_TOKEN_HERE"
keyword = "Paris"
```

## Model

### Search station by name


```python
def search_station_by_name(token, keyword):
    url = f"https://api.waqi.info/search/?keyword={keyword}&token={token}"
    res = requests.get(url)
    if res.status_code == 200:
        return res.json()

result = search_station_by_name(token, keyword)
```

### Create dataframe


```python
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

data = []
for d in result.get("data"):
    station = flatten_dict(d, parent_key='', sep='_')
    data.append(station)

df = pd.DataFrame(data)
```

## Output

### Display result


```python
print("➡️ Results found:", len(df))
df
```

 
