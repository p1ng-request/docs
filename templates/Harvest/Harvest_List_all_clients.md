**Tags:** #harvest #clients #api #list #python #get

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will list all clients from Harvest API and is usefull for organizations to get a list of their clients.

**References:**
- [Harvest API Documentation](https://help.getharvest.com/api-v2/clients-api/clients/clients/)
- [Harvest API Client Libraries](https://help.getharvest.com/api-v2/client-libraries/)

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

### List all clients

This function will list all clients from Harvest API.


```python
def list_clients(account_id, access_token, limit=-1):
    # Init
    data = []
    df = pd.DataFrame()
    
    # Requests
    url = "https://api.harvestapp.com/v2/clients"
    headers = {
        "Authorization": f"Bearer {access_token}",
        "Harvest-Account-ID": account_id,
        "User-Agent": "Harvest API Client",
        "Content-Type": "application/json",
    }
    
    # Loop on while
    while True:
        res = requests.get(url, headers=headers)
        if res.status_code == 200:
            # Get data
            res_json = res.json()
            tmp = res_json.get("clients")
            for t in tmp:
                data.append(t)
            
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
df_clients = list_clients(
    account_id,
    access_token,
    limit
)
print("Row fetched:", len(df_clients))
df_clients.head(1)
```

 
