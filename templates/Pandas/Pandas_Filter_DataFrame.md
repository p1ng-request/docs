<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Filter_DataFrame.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Filter+DataFrame:+Error+short+description">Bug report</a>

**Tags:** #pandas #dataframe #filter #python #dataanalysis

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to filter a DataFrame using Pandas.

**References:**
- [Tutorialspoint - Pandas](https://www.tutorialspoint.com/python_pandas/python_pandas_dataframe.htm)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables


```python
# Create a fake dataset
data = {
    "name": ["Jason", "Molly", "Tina", "Jake", "Amy"],
    "year": [2012, 2012, 2013, 2014, 2014],
    "reports": [4, 24, 31, 2, 3],
}
# Create a DataFrame
df = pd.DataFrame(data)
df
```

## Model

### Filter DataFrame

This will filter the DataFrame to only show the rows where the number of reports is greater than 4.


```python
# Filter the DataFrame
df_filtered = df.copy()
df_filtered = df_filtered[df_filtered["reports"] > 4]
df_filtered
```

## Output

### Display result


```python
# Display the filtered DataFrame
df_filtered
```

 
