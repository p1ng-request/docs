<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Sheets/Google_Sheets_Get_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #gsheet #data #naas_drivers

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

Pre-requisite: share your Google Sheet with our service account
For the driver to fetch the contents of your google sheet, you need to share it with the service account linked with Naas.

🔗 naas-share@naas-gsheets.iam.gserviceaccount.com

## Input

### Import library


```python
from naas_drivers import gsheet
```

### Variables


```python
spreadsheet_id = "---------"
```

## Model

### Connect to gsheet


```python
gsheet.connect(spreadsheet_id)
```

## Output

### Get the data


```python
gsheet.get(sheet_name="TSLA")
```
