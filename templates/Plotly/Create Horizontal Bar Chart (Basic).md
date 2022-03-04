<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>


# Plotly - Create Horizontal Bar Chart (Basic)
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Plotly/Create%20Horizontal%20Bar%20Chart%20%28Basic%29.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #plotly #chart #horizontalbar #dataviz

Learn more on the Plotly doc : https://plotly.com/python/horizontal-bar-charts/

## Input

### Import library


```python
import plotly.graph_objects as go
```

## Model

### Create the plot


```python
fig = go.Figure(go.Bar(
            x=[20, 14, 23],
            y=['giraffes', 'orangutans', 'monkeys'],
            orientation='h'))
```

## Output

### Display result


```python
fig.show()
```
