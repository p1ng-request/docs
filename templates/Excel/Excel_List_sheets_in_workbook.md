<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel/Excel_List_sheets_in_workbook.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Excel+-+List+sheets+in+workbook:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #excel #list #sheets #workbook #data #analysis

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will list the sheet's name in an Excel workbook.

**References:**
- [Python openpyxl](https://openpyxl.readthedocs.io/en/stable/)

## Input

### Import libraries


```python
import openpyxl
import os
```

### Setup Variables
- `file_path`: path of the Excel workbook
- `sheets`: list of sheets in Excel workbook


```python
# Inputs
file_path = "Conso.xlsx"

# Outputs
sheets = []
```

## Model

### List sheets in workbook
The load_workbook function loads the workbook into memory, and sheetnames property returns a list of sheet names in the workbook. Finally, we loop over the sheet names and print them out.


```python
if os.path.exists(file_path):
    # Load the workbook
    workbook = openpyxl.load_workbook(file_path)

    # Get the sheet names
    sheet_names = workbook.sheetnames

    # Print the sheet names
    for sheet_name in sheet_names:
        print(sheet_name)
        sheets += [sheet_name]
else:
    print(f"❌ Excel path '{file_path}' does not exist. Please update it on your variables.")
```

## Output

### Display result


```python
print(sheets)
```

 
