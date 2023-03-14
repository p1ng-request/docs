<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PyGWalker/PyGWalker_Analyze_Pandas_dataframe.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PyGWalker+-+Analyze+Pandas+dataframe:+Error+short+description">Bug report</a>

**Tags:** #pandas #dataframe #tableau #pygwalker #analyze #jupyter

**Author:** [Abraham Israel](https://www.linkedin.com/in/abraham-israel/)

**Description:** This notebook will demonstrate how to analyze a Pandas dataframe in Jupyter using a Tableau-style interface.

**References:**
- [Tableau Documentation](https://help.tableau.com/current/pro/desktop/en-us/data_analysis.htm)
- [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/index.html)

## Input

### Import libraries


```python
import pandas as pd
import numpy as np
try:
    import pygwalker as pyg
except:
    !pip install pygwalker --user
    import pygwalker as pyg
```

### Setup Variables
- `df`: Pandas dataframe to be analyzed


```python
df = pd.DataFrame(np.random.randint(0, 100, size=(100, 4)), columns=list("ABCD"))
```

## Model

### Analyze dataframe

This action will analyze the dataframe using a Tableau-style interface.


```python
# Analyze dataframe
df.describe()
```

## Output

### Display result


```python
# Display result
gwalker = pyg.walk(df)
```
