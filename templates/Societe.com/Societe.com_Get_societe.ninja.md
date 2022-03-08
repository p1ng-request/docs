<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Societe.com/Societe.com_Get_societe.ninja.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #companies #opendata #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

## Input

### Import library


```python
import pandas as pd
```

## Model

### Get the company details


```python
data = pd.read_html("https://societe.ninja/data.php?siren=437982937", encoding="UTF-8")
```


```python
print(len(data))
```

## Output

### Display result (You can change the index 0-7 for change the printed data)


```python
data[0].to_dict(orient="records")
```
