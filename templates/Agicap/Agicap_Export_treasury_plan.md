<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Agicap/Agicap_Export_treasury_plan.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Agicap+-+Export+treasury+plan:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #agicap #treasury #export #plan #finance #data #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook will export the Excel treasury plan consolidated by month from Agicap and return a dataframe.

**References:**
- [Agicap Website](https://app.agicap.com/fr/)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
from datetime import datetime
from dateutil.relativedelta import relativedelta
```

### Setup Variables
- `username`: Agicap username
- `password`: Agicap password
- `enterprise_id`: Agicap enterprise ID. Your Agicap account manager can provide you all your enterprises/accounts ids.
- `date_start`: First date of the extract in format: "%Y-%m-%d" (example: 2023-01-01). If not set it will return the first day of the current month
- `date_end`: Last date of the extract in format: "%Y-%m-%d" (example: 2023-01-31). If not set it will return the last day of the current month
- `output_csv`: csv file path to be saved as output


```python
# Inputs
username = naas.secret.get('AGICAP_USERNAME') or "<username>"
password = naas.secret.get('AGICAP_PASSWORD') or "<password>"
enterprise_id = "00001"
date_start = None
date_end = None

# Outputs
output_csv = f"ExportExcelSimple_{enterprise_id}.csv"
```

## Model

### Get token from Agicap
Get token using user credentials


```python
def get_token(
    username=None,
    password=None,
    force_update=False,
):
    # Get credentials
    if not username:
        username = naas.secret.get('AGICAP_USERNAME')
    if not password:
        password = naas.secret.get('AGICAP_PASSWORD')
        
    # Check if token exists
    token = naas.secret.get('AGICAP_TOKEN')
    if token and not force_update:
        return token
    
    # Sign in to get token
    url = "https://business-definition.agicap.com/signin"
    headers = {
        "Accept": "application/json, text/plain, */*",
        "Content-Type": "application/json"
    }
    payload = {
        "Username": username,
        "Password": password
    }
    res = requests.post(url, headers=headers, json=payload)
    res.raise_for_status
    
    # Get agicap token
    if len(res.json()) > 0:
        token = res.json().get("token")
        if token != naas.secret.get('AGICAP_TOKEN'):
            naas.secret.add('AGICAP_TOKEN', token)
    else:
        print('Error while connecting to AGICAP!')
    return token

token = get_token(username, password)
```

### Get date range
Transform date to timestamp to pass it as parameters in request.


```python
def get_date_range(
    date_start,
    date_end
):
    # Get first and last day of current month
    first_day_month = datetime.now().replace(day=1, hour=0, minute=0, second=0, microsecond=0)
    last_day_month = first_day_month + relativedelta(months=1) - relativedelta(seconds=1)
    
    # Setup range
    if not date_start:
        date_start = first_day_month
    else:
        date_start = datetime.strptime(date_start, "%Y-%m-%d")
        
    if not date_end:
        date_end = last_day_month
    else:
        date_end = datetime.strptime(date_end, "%Y-%m-%d")
        
    # Timestamp for requests with milliseconds
    ts_start = date_start.strftime("%s") + "000"
    ts_end = date_end.strftime("%s") + "000"
    return ts_start, ts_end

date_start_t, date_end_t = get_date_range(date_start, date_end)
```

### Export treasury plan
Get export with request


```python
def clean_excel(
    res,
    header=2
):
    # Read excel
    df = pd.read_excel(res.content, header=header)
    
    # Remove unnamed columns
    for c in df.columns:
        if c.startswith("Unnamed"):
            df = df.drop(c, axis=1)
            
    # Drop empty rows
    df = df.dropna()
    return df.reset_index(drop=True)

def get_excel_simple(
    enterprise_id,
    token,
    date_start=None,
    date_end=None
):
    # Init
    df = pd.DataFrame()
    
    # Payload
    payload = {
        "Scenarios":
        [
            {
                "Id": None,
                "colorSelected": False,
                "isEdit": False,
                "isLoading": False,
                "isSelected": True,
                "tableauDeBordPrevisionel": True,
                "forecastRawData": True
            }
        ],
        "DateBegin": date_start,
        "DateEnd": date_end,
        "Periodicite": {"Day": 0, "Month": 1}
    }
    # Headers
    headers = {
        "Accept": "application/json, text/plain, */*",
        "Accept-Language": "fr",
        "Authorization": f"Bearer {token}",
        "EntrepriseId": enterprise_id,
        "Content-Type": "application/json"
    }
    # Request
    url = "https://app.agicap.com/api/exportexcel/ExportExcelSimple"
    res = requests.post(url, headers=headers, json=payload)
    if res.status_code == 200:
        # Clean excel
        df = clean_excel(res)
    elif res.status_code == 401:
        token = get_token()
        headers["Authorization"] = f"Bearer {token}"
        res = requests.post(url, headers=headers, json=payload)
        df = clean_excel(res)
    else:
        print(res.status_code, res.text)
        print("❌ Error while getting:", url)
    return df.reset_index(drop=True)

df = get_excel_simple(
    enterprise_id,
    token=token,
    date_start=date_start_t,
    date_end=date_end_t
)
print("Rows fetched:", len(df))
df.head(5)
```

 

## Output

### Save export to CSV


```python
df.to_csv(output_csv, index=False)
```
