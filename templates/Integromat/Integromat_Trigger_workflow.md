<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Integromat - Trigger workflow
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Integromat/Integromat_Trigger_workflow.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #integromat

## Input

### Import library


```python
from naas_drivers import integromat
```

### Variables


```python
URL = "https://hook.integromat.com/7edtlwmn8foer0r9i9ainjvsz3vxmwos"
DATA = { "first_name":"Bryan", "last_name":"Helmig", "age": 27 }
```

## Model

### Connect to integromat


```python
result = integromat.connect(URL)
```

## Output

### Send data


```python
result = integromat.send(DATA)
```
