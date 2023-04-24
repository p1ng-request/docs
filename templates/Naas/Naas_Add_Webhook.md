<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Add_Webhook.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Add+Webhook:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #webhook #api #add #reference #docs

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to add a webhook using Naas feature. The notebook will be sent to production and you will get an URL that can be triggered.

Webhooks are useful because they enable real-time communication between applications, allowing for automated notifications or data exchange when specific events occur. This eliminates the need for constant polling and manual data retrieval, making webhooks efficient and scalable for various use cases.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Webhook Documentation](https://docs.naas.ai/features/api)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `path`: path of the notebook to be deploy in production. If no path is set, the current notebook will be sent to production.
- `notif_down`: List of emails. Receive an email when the notebook run fails. By default, you will received notifications on your email used on your naas account
- `notif_up`: List of emails. Receive an email when the notebook runs well. By default, you won't received notifications if it went well.


```python
path = None
notif_down = []
notif_up = []
```

## Model

### Add Webhook
Send in production this notebook and get URL to run it when opened.


```python
webhook_url = naas.webhook.add(path=path, params={"notif_down": notif_down, "notif_up": notif_up})
```

## Output

### Display result


```python
print("👌 Well done! Your Notebook has been sent to production:", webhook_url)
```

 
