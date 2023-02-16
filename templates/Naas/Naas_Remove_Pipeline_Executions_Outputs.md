<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Remove_Pipeline_Executions_Outputs.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Remove+Pipeline+Executions+Outputs:+Error+short+description">Bug report</a>

**Tags:** #naas #scheduler #automation #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook removes your production pipeline executions outputs automatically.

## Input

### Import libraries


```python
import glob
import os
import naas
from datetime import datetime
from dateutil.relativedelta import relativedelta
import shutil
```

### Setup Variables


```python
MONTH_LIMIT = 1
```

### Schedule your notebook


```python
# Schedule your notebook everyday at 9 AM
naas.scheduler.add(cron="0 9 * * *")

# -> Uncomment the line below to remove your scheduler
# naas.scheduler.delete()
```

## Model

### Get pipeline executions folders


```python
folders = glob.glob("/home/ftp/.naas/home/ftp/**/pipeline_executions/*", recursive=True)
print("Folders found:", len(folders))
folders[:1]
```

### Remove scheduler outputs.


```python
def remove_pipeline_executions(folders, limit):
    date_limit = (datetime.today() - relativedelta(months=limit)).strftime(
        "%Y%m%d%H%M%S"
    )
    for folder in folders:
        timestamp = folder.split("/")[-1][:19].replace("_", "").replace("-", "")
        if int(date_limit) > int(timestamp):
            shutil.rmtree(folder)
            print(f"✅ DELETED: {folder}")
```

## Output


```python
remove_pipeline_executions(folders, MONTH_LIMIT)
```
