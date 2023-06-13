<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Looping_Over_Dataframe.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Looping+Over+Dataframe:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #python #loops #dataframes #forloop #loop #snippet #operations

**Author:** [Oketunji Oludolapo](https://www.linkedin.com/in/oludolapo-oketunji/)

**Description:** This notebook provides an overview of multiples ways to use loops to iterate over a dataframe.

**References:**
- [Efficiently iterating over rows in a Pandas DataFrame](https://towardsdatascience.com/efficiently-iterating-over-rows-in-a-pandas-dataframe-7dd5f9992c01)

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

### Looping over the data to get the column name


```python
for column in df:
    print(column)
```

### Looping over the data to view the columns and their values sequentially


```python
for k, v in df.iteritems():
    print(k, v)
```

### Looping over dataframes to get the information about a row with respect to its columns


```python
for index, row in df.iterrows():
    print(index)
    print(row)
```

### Looping over dataframes to view the data per row as a tuple with the column values


```python
for row in df.itertuples():
    print(row)
```
