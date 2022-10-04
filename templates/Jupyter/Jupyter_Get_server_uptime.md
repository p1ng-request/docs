<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Jupyter/Jupyter_Get_server_uptime.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #jupyter #server #uptime #snippet #operations #naas

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

## Input

### Import libraries


```python
from naas_drivers import jupyter
from os import environ
```

### Setup your Jupyter


```python
# Jupyter token stored in your env
JUPYTER_TOKEN = environ.get('JUPYTERHUB_API_TOKEN')

# Username => email address linked to your jupyter account
username = "hello@naas.ai"
```

## Model

### Get server uptime


```python
data = jupyter.connect(JUPYTER_TOKEN).get_server_uptime(username)
```

## Output

### Display result


```python
data
```
