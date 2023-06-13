<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Read_CSV.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Read+CSV:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #csv #snippet #operation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook show how to read a CSV file.

**References:**
- [Pandas - Read CSV](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `file_path`: CSV file path
- `sep`: Delimiter to use. If sep is None, the C engine cannot automatically detect the separator, but the Python parsing engine can, meaning the latter will be used and automatically detect the separator by Python’s builtin sniffer tool, csv.Sniffer. 
- `header`: Row number(s) to use as the column names, and the start of the data.
- `encoding`: Encoding to use for UTF when reading/writing (ex. ‘utf-8’). [List of Python standard encodings](https://docs.python.org/3/library/codecs.html#standard-encodings).


```python
file_path = "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv"
sep = ","
header = 0
encoding = "utf-8"
```

## Model

### Read CSV


```python
df = pd.read_csv(
    file_path,
    sep=sep,
    header=header,
    encoding=encoding
)
df
```

## Output

### Display result


```python
print("Row fetched:", len(df))
df.head(1)
```
