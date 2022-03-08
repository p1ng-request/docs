<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Create%20Bubble%20chart.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #bubblechart #dataviz

Learn more on the Plotly doc : https://plotly.com/python/bubble-charts/

## Input

### Import library


```python
import plotly.express as px
```

## Model

### Bubble chart


```python
df = px.data.gapminder()

fig = px.scatter(df.query("year==2007"), x="gdpPercap", y="lifeExp",
	         size="pop", color="continent",
                 hover_name="country", log_x=True, size_max=60)
```

## Output

### Display result


```python
fig.show()
```
