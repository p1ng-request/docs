<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Create%20Line%20Chart%20%28Basic%29.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #linechart #trend #dataviz

Learn more on the Plotly doc : https://plotly.com/python/line-charts/

## Input

### Import library


```python
import plotly.express as px
```

## Model

### Create the plot


```python
df = px.data.gapminder().query("continent=='Oceania'")
fig = px.line(df, x="year", y="lifeExp", color='country')
```

## Output

### Display result


```python
fig.show()
```
