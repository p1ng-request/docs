<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Create_conditional_column_enrichment_using_DataFrame.loc.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Create+conditional+column+enrichment+using+DataFrame.loc:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datenrichment #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook demonstrates the practical application of `DataFrame.loc` for implementing conditions, enabling users to seamlessly enrich a DataFrame by generating new columns based on conditions derived from existing ones. Its versatility makes it an invaluable tool for DataFrame manipulation.

**References:**
- [Pandas - DataFrame.loc](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `new_column`: column label to be created


```python
new_column = "ranking"
```

## Model

### Create DataFrame


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

### Create new column


```python
df.loc[:, new_column] = "C" #apply condition on all rows with ':'
df.loc[(df["points"] >= 10) & (df["assists"] >= 5) & (df["rebounds"] >= 5), new_column] = "B"
df.loc[(df["points"] >= 10) & (df["assists"] >= 5) & (df["rebounds"] >= 10), new_column] = "A"
df.loc[(df["points"] >= 10) & (df["assists"] >= 10) & (df["rebounds"] >= 5), new_column] = "A"
```

## Output

### Display new DataFrame


```python
df
```


```python

```
