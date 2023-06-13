<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Save_dataframe_to_Excel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Save+dataframe+to+Excel:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #excel #snippet #operation #dataframe #save 

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook show how to save a dataframe to Excel.

**References:**
- [Pandas - Dataframe to Excel](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_excel.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `file_path`: Excel file path as output if you are using Naas it will start with `home/ftp/`
- `sheet_name`: Name of the sheet that will contain the DataFrame
- `index`: Specifies whether to write row names (index) to the Excel file. Boolean, default is True


```python
file_path = "/home/ftp/output.xlsx" 
sheet_name = "Name"
index = False
```

## Model

### Create dataframe


```python
# DataFrame creation
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

## Output

### Save DataFrame to Excel file


```python
# Saving the DataFrame in an Excel file
df.to_excel(file_path, sheet_name=sheet_name, index=index)
print(f"DataFrame successfully saved: {file_path}")
```
