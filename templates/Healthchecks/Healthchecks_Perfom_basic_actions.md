<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Healthchecks/Healthchecks_Perfom_basic_actions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Healthchecks+-+Perfom+basic+actions:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #healthchecks #snippet #operations

**Author:** [Martin Donadieu](https://www.linkedin.com/in/martindonadieu/)

**Description:** This notebook provides a set of basic actions to help monitor and maintain the health of a system.

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
