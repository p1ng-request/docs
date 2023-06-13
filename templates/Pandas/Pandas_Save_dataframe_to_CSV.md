<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Save_dataframe_to_CSV.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Save+dataframe+to+CSV:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #csv #snippet #operation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook show how to save a dataframe to a CSV file.

**References:**
- [Pandas - Save CSV](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `file_path`: CSV file path as output
- `sep`: Delimiter to use. If sep is None, the C engine cannot automatically detect the separator, but the Python parsing engine can, meaning the latter will be used and automatically detect the separator by Python’s builtin sniffer tool, csv.Sniffer. 
- `header`: Row number(s) to use as the column names, and the start of the data.
- `encoding`: Encoding to use for UTF when writing (ex. ‘utf-8’). [List of Python standard encodings](https://docs.python.org/3/library/codecs.html#standard-encodings).
- `index`: Write row names (index). Boolean default True


```python
file_path = "output.csv"
sep = ","
header = 0
encoding = "utf-8"
index = False
```

## Model

### Create dataframe


```python
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

### Display result


```python
df.to_csv(file_path)
print(f"DataFrame successfully saved: {file_path}")
```
