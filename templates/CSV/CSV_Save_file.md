<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/CSV/CSV_Save_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=CSV+-+Save+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #csv #pandas #save #opendata #johnshopkins #investors #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides instructions on how to save a file in CSV format.

## Input

### Import library


```python
import pandas
```

### Variable


```python
# Input
csv_path = "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv"

# Output
csv_output_path = "data.csv"
```

## Model

### Read the CSV from path

You want to add more parameters ?<br>
👉 Check out the pandas documentation <a href="https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html">here</a>.


```python
df = pandas.read_csv(csv_path)
df
```

## Output

You want to add more parameters ?<br>
👉 Check out the pandas documentation <a href="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html">here</a>.


```python
df.to_csv(csv_output_path)
print(f'💾 Excel '{csv_output_path}' successfully saved in Naas.')
```
