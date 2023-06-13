<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_List_Schedulers_with_last_execution.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+List+Schedulers+with+last+execution:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #schedulers #list #production #tool #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to list current schedulers running in production with their last execution meta data and return a dataframe.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Asset Documentation](https://docs.naas.ai/features/scheduler)

## Input

### Import libraries


```python
import naas
import pandas as pd
```

## Model

### List current Schedulers


```python
schedulers = naas.scheduler.currents(raw=True)
schedulers[0]
```

## Output

### Display result


```python
df = pd.DataFrame(schedulers).drop("runs", axis=1)
print("Scheduler fecthed:", len(df))
df
```

 
