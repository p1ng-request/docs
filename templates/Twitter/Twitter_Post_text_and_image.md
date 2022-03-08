<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twitter/Twitter_Post_text_and_image.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #twitter #automation #ifttt #naas_drivers

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

## Input

### Import libraries


```python
import naas
import naas_drivers
```

## Model

### Get data from yahoofinance


```python
data = naas_drivers.yahoofinance.get('^FCHI',date_from=-200, moving_averages=[50,20])
```


```python
chart = naas_drivers.plotly.stock(data)
chart.show()
```


```python
name = "chart.png"
naas_drivers.plotly.export(chart, name)
```


```python
url = naas.assets.add(name, params={"inline":True})
```

### Let's write the post


```python
twitter_post = """📈🚀 Every day at 9AM PST / 6PM CET<br>
CAC40 index value with #MovingAverages 20 and 50
<br>
Don't miss an #opportunity to #invest<br>
<br>
PS : this post has been generated automatically with https://www.naas.ai/ 😎 
#automation #trading #data #analysis @Nasdaq
"""
event = "twitter-post"
key = "ke4AigvXI5-EABaowdLt4fju1aOUxeMxSXQoN8FVyA"
data = { "value1" : twitter_post,  "value2" : url}
```

## Output

### Post data


```python
result = naas_drivers.ifttt.webhook(event, key, data)
```
