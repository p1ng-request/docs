    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Zapier/Zapier_Trigger_workflow.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Zapier+-+Trigger+workflow:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #zapier #nocode #operations #snippet

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows you to create automated workflows that are triggered by specific events.

## Input

### Import library


```python
import naas_drivers
```

## Model

### Variables


```python
url = "https://zapier.com/hooks/catch/n/Lx2RH/"
data = {"first_name": "Bryan", "last_name": "Helmig", "age": 27}
```

## Output

### Display result


```python
result = naas_drivers.zappier.connect(url).send(data)
```
