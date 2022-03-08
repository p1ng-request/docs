<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Zapier/Zapier_Trigger_workflow.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #zapier #automation #nocode

## Input

### Import library


```python
import naas_drivers
```

## Model

### Variables


```python
url = "https://zapier.com/hooks/catch/n/Lx2RH/"
data = { "first_name":"Bryan", "last_name":"Helmig", "age": 27 }
```

## Output

### Display result


```python
result = naas_drivers.zappier.connect(url).send(data)
```
