<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Newsapi/Newsapi_Run_sentiment_analysis.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Newsapi+-+Run+sentiment+analysis:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #newsapi #news #sentimentanalysis #ai #opendata #dataframe

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook uses Newsapi to analyze the sentiment of news articles.

## Input

### Import libraries


```python
from naas_drivers import newsapi, sentiment
```

## Model

### Connect to newsAPI and get the data


```python
data = newsapi.connect().get(
    "bitcoin", fields=["title", "image", "link", "description"]
)
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
