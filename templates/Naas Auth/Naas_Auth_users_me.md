<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas%20Auth/Naas_Auth_users_me.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+Auth+-+Users+me:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naasauth #naas #auth #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

**Description:** This notebook provides a user-friendly interface for authenticating users with Naas.

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
