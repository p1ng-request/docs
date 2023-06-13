<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Jupyter/Jupyter_Get_user_information.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Jupyter+-+Get+user+information:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #jupyter #user #snippet #operations #naas

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides a way to retrieve user information from Jupyter.

## Input

### Import libraries


```python
from naas_drivers import jupyter
from os import environ
```

### Setup your Jupyter


```python
# Jupyter token
JUPYTER_TOKEN = environ.get("JUPYTERHUB_API_TOKEN")
```

## Model

### Get user information


```python
data = jupyter.connect(JUPYTER_TOKEN).get_me()
```

## Output

### Display result


```python
data
```
