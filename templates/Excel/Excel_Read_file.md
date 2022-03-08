<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel/Excel_Read_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #excel #pandas #read

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

## Input

### Import libraries


```python
import pandas as pd 
```

### Variables


```python
excel_file_path = "Excel-Sales_Jan2020.xlsx"
```

## Model

### Read excel

You want to add more parameters ?<br>
👉 Check out the pandas documentation <a href="https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html">here</a>.


```python
df = pd.read_excel(excel_file_path)
```

## Output

### Display result


```python
df
```
