<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Naas Auth - Connect
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas%20Auth/Naas_Auth_connect.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #auth

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

## Input

### Import library


```python
from naas_drivers import naasauth
```

## Model

### Function

When calling connect() you can either pass a token generated [here](https://app.naas.ai/hub/token) or pass nothing. If you choose to pass nothing and that you are running this notebook on [app.naas.ai](https://app.naas.ai) it will use your jupyter token automatically.


```python
#naasauth.connect(token="yourjupyterhubtoken")
#naasauth.connect("yourjupyterhubtoken")
naasauth.connect()
```

## Output

### Display result


```python
naasauth.access_token
```


```python
naasauth.headers
```
