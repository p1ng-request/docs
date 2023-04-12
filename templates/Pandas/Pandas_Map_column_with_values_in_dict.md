    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Map_column_with_values_in_dict.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Map+column+with+values+in+dict:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dict #map #series

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to map a column of a Pandas DataFrame with values from a dictionary.

<u>References:</u>
- https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.map.html
- https://www.geeksforgeeks.org/python-pandas-dataframe-map/

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables


```python
data = {"Name": ["John", "Paul", "George", "Ringo"], "Age": [20, 21, 19, 18]}
mapping_dict = {20: "Young", 21: "Young", 19: "Adult", 18: "Adult"}
```

## Model

### Read dataframe


```python
df = pd.DataFrame(data)
df
```

### Map column with values in dict


```python
df["Age_Group"] = df["Age"].map(mapping_dict)
```

## Output

### Display result


```python
df
```
