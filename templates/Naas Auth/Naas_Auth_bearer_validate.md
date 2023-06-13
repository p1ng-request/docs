<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas%20Auth/Naas_Auth_bearer_validate.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+Auth+-+Bearer+validate:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naasauth #naas #auth #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

**Description:** This notebook provides a way to validate Bearer tokens for authentication with the Naas API.

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
naasauth.bearer.validate()
```


```python

```
