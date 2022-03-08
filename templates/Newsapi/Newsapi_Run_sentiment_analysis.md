<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Newsapi/Newsapi_Run_sentiment_analysis.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #newsapi #news #sentimentanalysis

## Input

### Import library


```python
from naas_drivers import newsapi
from naas_drivers import sentiment
```

## Model

### Connect to newsAPI and get the data


```python
data = newsapi.connect().get("bitcoin", fields=["title", "image", "link", "description"])
```

### Get sentiment analysis


```python
sentiment = sentiment.get(data, column_name="title")
```

## Output

### Display results


```python
data
```


```python
sentiment
```
