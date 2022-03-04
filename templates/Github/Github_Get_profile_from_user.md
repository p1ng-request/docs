<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Github - Get profile from user
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Github/Github_Get_profile_from_user.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

This notebook enables you to get a dataframe of all the stargazzers of a particular Github repository.

**Tags:** #github #user #profile

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

## Input

### Imports


```python
import pandas as pd
import requests
import os
from urllib.parse import urlencode
```

### Variables


```python
USER_URL = "https://github.com/FlorentLvr"
GITHUB_TOKEN = "ghp_Stz3qlkR3b00nKUW8rxJoxxxxxxxxxxxx"
```

## Model

### Get profile from user


```python
def get_profile(html_url, url=None):
    if url is None:
        user = html_url.split("github.com/")[-1].split("/")[0]
        url = f"https://api.github.com/users/{user}"
    headers = {'Authorization': f'token {GITHUB_TOKEN}'}
    res = requests.get(url, headers=headers)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        raise(e)
    res_json = res.json()

    # Dataframe
    df = pd.DataFrame([res_json])
    for col in df.columns:
        if col.endswith("url"):
            df = df.drop(col, axis=1)
        if col.endswith("_at"):
            df[col] = df[col].str.replace("T", " ").str.replace("Z", " ")
    return df

df_user = get_profile(USER_URL)
```

## Output

### Display result


```python
df_user
```
