<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel/Excel_Read_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Excel+-+Read+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #excel #pandas #read #finance #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook reads an Excel file and allows users to manipulate the data within it.

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
