<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Groupby_and_Aggregate.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Groupby+and+Aggregate:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #snippet #datamining #dataaggragation #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook groups and perform aggregation on columns.

**References:**
- [Pandas - Groupby](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)
- [Pandas - Aggregate](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.agg.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `to_group`: list of columns to group
- `to_agg`: dict of columns to aggregate, accepted combinations are function, string function name: "sum", "count", "mean", list of functions and/or function names, e.g. [np.sum, 'mean'], dict of axis labels -> functions, function names or list of such.


```python
# list of columns to group
to_group = ["team"]

# dict of columns to aggregate
to_agg = {
    "points": "sum",
    "assists": "sum",
    "rebounds": "sum",
}
```

## Model

### Create DataFrame


```python
# create DataFrame
df = pd.DataFrame(
    {
        "team": ["A", "A", "A", "B", "B", "B"],
        "points": [11, 7, 8, 10, 21, 13],
        "assists": [5, 7, 7, 9, 12, 0],
        "rebounds": [5, 8, 10, 6, 6, 22],
    }
)
df
```

### Groupby and Aggregate columns
- When you use .groupby() function on any categorical column of DataFrame, it returns a GroupBy object. Then you can use different methods on this object and even aggregate other columns to get the summary view of the dataset.
- The agg() method allows you to apply a function or a list of function names to be executed along one of the axis of the DataFrame, default 0, which is the index (row) axis.


```python
# For aggregated output, return object with group labels as the index.
# Only relevant for DataFrame input. as_index=False is effectively “SQL-style” grouped output.
df = df.groupby(by=to_group, as_index=False).agg(to_agg)
```

## Output

### Display new DataFrame


```python
df
```
