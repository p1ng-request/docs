<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Excel%20365/Access%20Excel%20365%20sheet.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #excel365 #snippet

**Author:** [Ebin Paulose](https://www.linkedin.com/in/ebinpaulose/)

## Input

### Import sharepoint connector


```python
try:
    import sharepoint_connector
except:
    !pip install sharepy
    import sharepoint_connector
```

### Set variables
- username - username of sharepoint account
- password - password of sharepoint account
- domain - domain of sharepont account (eg mysite.sharepoint.com)
- path - its a full path of file in sharepoint . 
  it can get from sharepoint dashbord by right click on file and select detail. 
  then path can copy from right panel in dashboard 
- sheet - name of sheet
- export -  it is an optional parameter. it can be csv or xlsx. file will be exported to data_output folder based on this variable. set export as empty string or False if no need to export the file


```python
password="9aXgzH2DRqKCCU8z"
username="jeremy.ravenel@cashstory.com"
domain = "cashstory.sharepoint.com"
path = "https://cashstory.sharepoint.com/sites/cashstory-external/Documents%20partages/CashStory%20Forecasting%20Module/Forecast.xlsx"
sheet = "Forecast"
export = "xls"  
```

## Model

### Connect to sharepoint with the variables


```python
df  = sharepoint_connector.connect(username, password, domain, path, sheet, export)
```

## Output

### Display result


```python
df
```
