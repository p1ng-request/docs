<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Healthchecks - Healthcheks Perfom basic actions
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Healthchecks/Healthcheks_Perfom_basic_actions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #healthchecks

Get notified of your Cron jobs

**Tags:** #healthchecks

## Input

### Import library


```python
from naas_drivers import healthcheck
```

### Variables


```python
url = "https://google.com"
key = "123456-123456-12455"
```

## Model

### Connect to healthcheck


```python
healthcheck.connect(key)
```

## Output

### Starting


```python
healthcheck.send("start")
```

### Done


```python
healthcheck.send()
```

### Failing


```python
healthcheck.send("fail")
```

### Check status UP


```python
healthcheck.check_up(url)
```
