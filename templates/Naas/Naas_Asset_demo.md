<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Asset_demo.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #asset #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

Read the doc on https://naas.gitbook.io/naas/features/asset

Build notebooks that can communicate with third parties applications and run remotely.

## Input

### Import library


```python
import naas 
```

## Model

### Path of your document


```python
PATH = "PATH_OF_YOUR_DOCUMENT.png"
```

## Output

### Add your asset


```python
naas.asset.add("YOUR_DOCUMENT.png")
```
