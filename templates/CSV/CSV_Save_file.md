<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# CSV - Save file
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/CSV/CSV_Save_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #csv #pandas #save #opendata #johnshopkins

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
