<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Thinkific/Thinkific_Send_users.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #thinkific #education #naas_drivers

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

### Connect to the API


```python
thinkific.connect(api_key)
```

## Output

### Send the user


```python
thinkific.users.send(
    email="bob@cashstory.com"
)
```
