<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Thinkific/Thinkific_Get_users.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #thinkific #education #naas_drivers #operations #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import thinkific
```

### Variables


```python
api_key = "api_key"
```

## Model

### Get users


```python
data = thinkific.connect(api_key).users.get(uid="uid")
```

## Output

### Display result


```python
data
```
