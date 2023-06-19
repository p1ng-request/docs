<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Sort_values_by_multiples_columns.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Sort+values+by+multiples+columns:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #sort #columns #values #multiples

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will show how to sort values by multiples columns in Pandas. It is usefull for data analysis and data manipulation.

**References:**
- [Pandas - Sort values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html)
- [Pandas - Tutoriel Sort Value](https://www.geeksforgeeks.org/python-pandas-dataframe-sort_values-set-2/)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables

- `by`: Name or list of names to sort by.
- `ascending`: bool or list of bool, default True. Specify list for multiple sort orders. If this is a list of bools, must match the length of the by.
- `ignore_index`: bool, default False. If True, the resulting axis will be labeled 0, 1, …, n - 1.


```python
by = ['Score', 'Age']
ascending = [False, True]
ignore_index = True
```

## Model

### Create a dataframe


```python
# Create a dataframe
data = {
    "Name": ["Tom", "nick", "krish", "jack"],
    "Age": [20, 21, 19, 18],
    "Score": [99, 98, 95, 90],
}
df = pd.DataFrame(data)
df
```

## Output

### Sort values by multiples columns


```python
# Sort the DataFrame by multiple columns
sorted_df = df.sort_values(by=by, ascending=ascending, ignore_index=ignore_index)
sorted_df
```

 
