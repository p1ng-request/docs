<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_List_Webhooks.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+List+Webhooks:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #asset #snipet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Webhook Documentation](https://docs.naas.ai/features/api)

**Description:** This notebook will show how to list current webhooks in production.

## Input

### Import libraries


```python
import naas
```

## Model

### List current Webhooks


```python
webhooks = naas.webhook.currents()
```

## Output

### Display result


```python
webhooks
```

 
