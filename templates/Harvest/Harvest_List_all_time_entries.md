<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Harvest/Harvest_List_all_time_entries.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Harvest+-+List+all+time+entries:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #harvest #timeentries #api #list #python #v2

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will list all time entries from the Harvest API v2. It is usefull for organizations to quickly access and display time entries.

**References:**
- [Harvest API v2 - Time Entries](https://help.getharvest.com/api-v2/timesheets-api/timesheets/time-entries/)
- [Harvest API v2 - Authentication](https://help.getharvest.com/api-v2/authentication-api/authentication/authentication/)

## Input

### Import libraries


```python
import requests
import pandas as pd
import naas
```

### Setup Variables
[Create your personnal access tokens](https://id.getharvest.com/oauth2/access_tokens/new)
- `account_id`: Account ID from Harvest
- `access_token`: Access token from Harvest
- `limit`: entries limit, to get all entries enter -1


```python
account_id = naas.secret.get("HARVEST_ACCOUNT_ID") or "YOUR_HARVEST_ACCOUNT_ID"
access_token = naas.secret.get("HARVEST_ACCESS_TOKEN") or "YOUR_HARVEST_ACCESS_TOKEN"
limit = 1000
```

## Model

### List all time entries

This function will list all time entries from the Harvest API v2.


```python
# Flatten the nested dict
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

def list_time_entries(account_id, access_token, limit=-1):
    # Init
    data = []
    df = pd.DataFrame()
    
    # Requests
    url = f"https://api.harvestapp.com/v2/time_entries?account_id={account_id}"
    headers = {
        "Authorization": f"Bearer {access_token}",
        "Harvest-Account-Id": account_id,
        "User-Agent": "Harvest API Python Client",
        "Content-Type": "application/json",
    }
    
    # Loop on while
    while True:
        res = requests.get(url, headers=headers)
        if res.status_code == 200:
            # Get data
            res_json = res.json()
            time_entries = res_json.get("time_entries")
            for time_entry in time_entries:
                data.append(flatten_dict(time_entry))
            
                # Manage limit
                if limit != -1 and len(data) >= limit:
                    break
                
            # Check next link
            link_next = res_json.get("links").get("next")
            if link_next:
                url = link_next
            else:
                break
            
    # Transform in dataframes
    df = pd.DataFrame(data)
    return df
```

## Output

### Display result


```python
df_time_entries = list_time_entries(
    account_id,
    access_token,
    limit
)
print("Row fetched:", len(df_time_entries))
df_time_entries.head(1)
```

 
