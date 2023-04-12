<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel/Excel_Consolidate_files.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Excel+-+Consolidate+files:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #excel #pandas #read #save #naas #asset #finance #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides a comprehensive guide to consolidating multiple Excel files into one.

## Input

### Import libraries


```python
import pandas as pd
import naas
```

### Variables


```python
# Input
excel_file_path1 = "Excel-Sales_Jan2020.xlsx"
excel_file_path2 = "Excel-Sales_Jan2020.xlsx"

# Output
excel_output_path = "Conso.xlsx"
```

## Model

### Read the 2 Excel files

You want to add more parameters ?<br>
👉 Check out the pandas documentation <a href="https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html">here</a>.


```python
df1 = pd.read_excel(excel_file_path1)
df1
```


```python
df2 = pd.read_excel(excel_file_path2)
df2
```

### Consolidate Excel


```python
df_concat = pd.concat([df1, df2], axis=0).reset_index(drop=True)
df_concat
```

## Output

### Save dataframe to Excel

You want to add more parameters ?<br>
👉 Check out the pandas documentation <a href="https://pandas.pydata.org/docs/reference/api/pandas.read_excel.html">here</a>.


```python
df_concat.to_excel(excel_output_path)
print(f'💾 Excel '{excel_output_path}' successfully saved in Naas.')
```

### Share excel with Naas


```python
naas.asset.add(excel_output_path)
```
