<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Jupyter - Get user information
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Jupyter/Jupyter_Get_user_information.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #jupyter

## Input

### Import library


```python
from naas_drivers import jupyter
```

### Variables


```python
token = "*********"
```

## Model

### Connect to jupyter


```python
jp = jupyter.connect(token)
```

## Output

### Get the user


```python
me = jp.get_me()
me
```


```python
uptime = jp.get_me_uptime()
uptime
```
