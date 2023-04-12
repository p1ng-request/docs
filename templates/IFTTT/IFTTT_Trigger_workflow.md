    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/IFTTT/IFTTT_Trigger_workflow.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=IFTTT+-+Trigger+workflow:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #ifttt #nocode #snippet #marketing

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to create automated workflows based on triggers from IFTTT.

## Input

### Import library


```python
from naas_drivers import ifttt
```

### Variables


```python
event = "myevent"
key = "cl9U-VaeBu1**********"
data = {"value1": "Bryan", "value2": "Helmig", "value3": 27}
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
