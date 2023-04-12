    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Add_Scheduler.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Add+Scheduler:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #scheduler #snippet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to automate a notebook using the scheduler feature of Naas.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Scheduler Documentation](https://docs.naas.ai/features/scheduler)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `path`: path of the notebook to be deploy in production. If no path is set, the current notebook will be sent to production.
- `cron`: We use CRON tasks to schedule notebooks, find the syntax you need to on: https://crontab.guru/
- `notif_down`: List of emails. Receive an email when the notebook run fails. By default, you will received notifications on your email used on your naas account
- `notif_up`: List of emails. Receive an email when the notebook runs well. By default, you won't received notifications if it went well.


```python
path = None
cron = "0 9 * * *"
notif_down = []
notif_up = []
```

## Model

### Add Scheduler


```python
naas.scheduler.add(path=path, cron=cron, params={"notif_down": notif_down, "notif_up": notif_up})
```

## Output

### Display result


```python
print("👌 Well done! Your Notebook has been sent to production.")
```
