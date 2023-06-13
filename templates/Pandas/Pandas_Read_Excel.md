<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Read_Excel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Read+Excel:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #excel #snippet #operation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook show how to read a Excel file.

**References:**
- [Pandas - Read Excel](https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `file_path`: Excel file path
- `sheet_name`: Strings are used for sheet names.


```python
file_path = ""
sheet_name = ""
```

## Model

### Read Excel


```python
df = pd.read_excel(file_path, sheet_name=sheet_name)
df
```

## Output

### Display result


```python
print("Row fetched:", len(df))
df.head(1)
```
