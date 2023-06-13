<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel/Excel_Get_dynamic_active_range.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Excel+-+Get+dynamic+active+range:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #excel #openpyxl #active-range #finance #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides a method for dynamically retrieving the active range of an Excel worksheet.

## Input

### Import libraries


```python
from openpyxl import load_workbook
from openpyxl.utils import get_column_letter
```

### Setup your Excel parameters


```python
excel_path = "Excel_Template.xlsx"
```

## Model

### Load Excel file and get active ws object


```python
wb = load_workbook(excel_path)
ws = wb.active
ws
```

### Get active range


```python
def get_active_range(ws):
    max_row = ws.max_row
    max_col = get_column_letter(ws.max_column)
    active_range = f"A1:{max_col}{max_row}"
    return active_range


active_range = get_active_range(ws)
```

## Output

### Display result


```python
active_range
```


```python

```
