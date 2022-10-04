<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas%20Auth/Naas_Auth_users_me.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naasauth #naas #auth #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

## Input

### Import library


```python
from naas_drivers import naasauth
```

## Model

### Function


```python
naasauth.connect()
```

## Output

### Display result


```python
naasauth.user.me()
```
