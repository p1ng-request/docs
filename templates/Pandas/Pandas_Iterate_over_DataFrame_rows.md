<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Iterate_over_DataFrame_rows.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Iterate+over+DataFrame+rows:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #python #loops #snippet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook demonstrates how to iterate over DataFrame rows as (index, Series) pairs.

**References:**
- [Pandas - DataFrame.iterrows](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.iterrows.html)

## Input

### Import libraries


```python
import pandas as pd
import numpy as np
```

## Model

### Create Sample Dataframe 


```python
dict1 = {
    "student_id": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    "student_name": [
        "Peter",
        "Dolly",
        "Maggie",
        "David",
        "Isabelle",
        "Harry",
        "Akin",
        "Abbey",
        "Victoria",
        "Sam",
    ],
    "student_course": np.random.choice(["Biology", "Physics", "Chemistry"], size=10),
}
df = pd.DataFrame(dict1)
df
```

## Output

### Display result


```python
for index, row in df.iterrows():
    print("Index:", index)
    for col in df.columns:
        print("Column:", col, "Value:", row[col])
```
