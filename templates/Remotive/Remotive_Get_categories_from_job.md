<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Remotive/Remotive_Get_categories_from_job.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Remotive+-+Get+categories+from+job:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #remotive #categories #snippet #opendata #dataframe

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook provides a way to categorize jobs posted on Remotive.

## Input

### Imports


```python
import pandas as pd
import requests
```

## Model

### Get categories from Remotive


```python
def get_remotejob_categories():
    req_url = f"https://remotive.io/api/remote-jobs/categories"
    res = requests.get(req_url)
    try:
        res.raise_for_status()
    except requests.HTTPError as e:
        return e
    res_json = res.json()

    # Get categories
    jobs = res_json.get("jobs")
    return pd.DataFrame(jobs)


df_categories = get_remotejob_categories()
```

## Output

### Display result


```python
df_categories
```
