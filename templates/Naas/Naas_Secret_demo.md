<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Secret_demo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #secret #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

Read the doc: https://naas.gitbook.io/naas/features/secret

**Tags:** #naas #secret

## Input

### Import library


```python
import naas
```

## Model

### Variable for the secret


```python
API_NAME = "HUBSPOT"
API_KEY = "123456789"
```

## Output

### Add the secret


```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```
