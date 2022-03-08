<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Societe.com/get_societe.ninja.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #companies #opendata

## Input

### Import library


```python
import pandas as pd
```

## Model

### Get the company details


```python
data = pd.read_html("https://societe.ninja/data.php?siren=880612569", encoding="UTF-8")
```


```python
print(len(data))
```

## Output

### Display result (You can change the index 0-7 for change the printed data)


```python
data[0]
```
