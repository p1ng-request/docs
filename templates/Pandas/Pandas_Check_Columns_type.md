    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Check_Columns_type.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Check+Columns+type:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook checks columns in a dataframe. It could be very usefull to apply specific rules regarding columns format.

## Input

### Import libraries


```python
import pandas as pd
```

### Setup DataFrame


```python
# create DataFrame
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", "B"],
        "points": [11, 7, 8, 10, 13, 13],
        "assists": [5, 7, 7, 9, 12, 9],
        "rebounds": [11, 8, 10, 6, 6, 5],
    }
)
df
```

### View DataFrame format


```python
df.info()
```

## Model

### Check Columns type in dataframe and create conditions


```python
for c in df.columns:
    print(f"Columns '{c}' is {df[c].dtype}.")
    if df[c].dtype == object:
        print(f"=> Do something")
    elif df[c].dtype == str:
        print(f"=> Do something")
    elif df[c].dtype == int:
        print(f"=> Do something")
    elif df[c].dtype == float:
        print(f"=> Do something")
```

## Output

### View new DataFrame format


```python
df.info()
```
