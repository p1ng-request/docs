<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Societe.com/Societe.com_Get_company_details.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #societe.com #companies #opendata #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

## Input

### Import library


```python
import pandas as pd
```

## Model

### Get the company details


```python
data = pd.read_html("https://www.societe.com/societe/cashstory-880612569.html")
```

## Output

### Display result


```python
data[0]
```


```python

```
