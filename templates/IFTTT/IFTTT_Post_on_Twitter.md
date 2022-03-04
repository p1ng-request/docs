<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# IFTTT - Post on Twitter
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/IFTTT/IFTTT_Post_on_Twitter.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #ifttt #automation #nocode

See the tutorial video on Youtube: https://www.youtube.com/watch?v=FvAM1aS4GFM

**Tags:** #ifttt #automation #nocode

## Input

### Import library


```python
from naas_drivers import ifttt
```

### Variables


```python
twitter_post = """Hello world, this is my first automated post 
                with @JupyterNaas @IFTTT driver🔥
                """
event = "naas_demo"
key = "ke4AigvXI5-EABaowdLt4fju1aOUxeMxSXQoN***"
data = { "value1": twitter_post }
```

## Model

### Connect to IFTTT


```python
result = ifttt.connect(key)
```

## Output

### Display result


```python
result = ifttt.send(event, data)
```
