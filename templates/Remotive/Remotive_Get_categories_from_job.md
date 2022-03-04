<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Remotive - Get categories from job
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Remotive/Remotive_Get_categories_from_job.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #remotive #categories

## Input

### Imports


```python
import pandas as pd
import requests
```

### Variables


```python
REMOTIVE_API = "https://remotive.io/api/remote-jobs"
```

## Model

### Get categories from Remotive


```python
def get_remotejob_categories(url):
    req_url = f"{url}/categories"
    res = requests.get(req_url)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        return e
    res_json = res.json()
    
    # Get categories
    jobs = res_json.get('jobs')
    return pd.DataFrame(jobs)

df_categories = get_remotejob_categories(REMOTIVE_API)
```

## Output

### Display result


```python
df_categories
```
