<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# IFTTT - Trigger workflow
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/IFTTT/IFTTT_Trigger_workflow.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #ifttt #automation #nocode

## Input

### Import library


```python
from naas_drivers import ifttt
```

### Variables


```python
event = "myevent"
key = "cl9U-VaeBu1**********"
data = { "value1": "Bryan", "value2": "Helmig", "value3": 27 }
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
