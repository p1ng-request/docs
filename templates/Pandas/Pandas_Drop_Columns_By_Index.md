    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Drop_Columns_By_Index.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Drop+Columns+By+Index:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Sunny Chugh](https://www.linkedin.com/in/sunny-chugh-ab1630177/)

**Description:** This notebook shows how to drop columns in Pandas DataFrame by index.

<u>Reference:</u> https://www.statology.org/pandas-drop-column-by-index/

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
        "team": ["Mavs", "Lakers", "Spurs", "Cavs"],
        "first": ["Dirk", "Kobe", "Tim", "Lebron"],
        "last": ["Nowitzki", "Bryant", "Duncan", "James"],
        "points": [26, 31, 22, 29],
    }
)
df
```

## Model

### Method : Use drop
The following code shows how to use the drop() function to drop the multiple columns of the pandas DataFrame by index.


```python
# Copy init dataframe
df1 = df.copy()
cols = [0, 1, 3]
df1.drop(df1.columns[cols], axis=1, inplace=True)
print(df1)
```

## Output

### Display result


```python
columns_dropped = ""
for column in cols:
    columns_dropped = columns_dropped + df.columns[column] + ", "
print("The Columns- " + columns_dropped + "are removed from dataframe")
```
