<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_List_Schedulers_with_all_executions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+List+Schedulers+with+all+executions:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #schedulers #list #production #tool #library

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to list current schedulers running in production with all their executions meta data and return a dataframe.

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

### Get all executions


```python
df = pd.DataFrame()

for scheduler in schedulers:
    runs = scheduler.get('runs')
    tmp_df = pd.DataFrame(runs)
    tmp_df.insert(loc=0, column="path", value=scheduler.get("path"))
    df = pd.concat([df, tmp_df]).reset_index(drop=True)
```

## Output

### Display result


```python
print("Executions fetched:", len(df))
print("No schedulers:", len(df["path"].unique()))
df.head(3)
```

 
