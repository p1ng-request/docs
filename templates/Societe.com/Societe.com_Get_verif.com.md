<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Societe.com/Societe.com_Get_verif.com.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #companies #opendata

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

## Input

### Import library


```python
import pandas as pd
```

## Model

### Get company data


```python
data = pd.read_html("https://www.verif.com/societe/CASHSTORY-880612569/", encoding="UTF-8")
```


```python
print(len(data))
```

## Output

### Display result (You can change your index 0-4)


```python
data[0]
```


```python

```
