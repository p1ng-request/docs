<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Fill_emtpy_values.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Fill+emtpy+values:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook fill empty values in dataframe columns.

**References:**
- [Pandas - Fillna](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html)

## Input

### Import libraries


```python
import pandas as pd
import numpy as np
```

### Setup Variables
- `to_fillna`: dict of columns with value to fill


```python
# dict of columns with value to fill
to_fillna = {"team": "Unknown team", "points": 0, "assists": 0, "rebounds": 0}
```

## Model

### Create DataFrame


```python
# create DataFrame
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", np.NaN],
        "points": [11, 7, 8, 10, np.NaN, 13],
        "assists": [5, 7, 7, 9, 12, np.NaN],
        "rebounds": [np.NaN, 8, 10, 6, 6, np.NaN],
    }
)
df
```

### Fill empty values in dataframe


```python
df = df.fillna(to_fillna)
```

## Output

### Display new DataFrame


```python
df
```
