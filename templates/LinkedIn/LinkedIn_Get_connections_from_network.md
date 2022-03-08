<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_connections_from_network.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #network #connections #naas_drivers #csv #analytics

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import linkedin
import naas
```

### Get your cookies
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

### Variables


```python
# Outputs
csv_output = "LinkedIn_connections.csv"
```

## Model

Get the information return in a dataframe.<br><br>
**Available columns :**
- PROFILE_URN : LinkedIn unique profile id
- CREATED_AT : Date of connection between and your connection
- PROFILE_ID : LinkedIn public profile id
- FIRSTNAME : First name
- LASTNAME : Last name
- OCCUPATION : Text below the name in the profile page


```python
df = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(limit=-1)
df
```

## Output

### Save dataframe in CSV


```python
df.to_csv(csv_output, index=False)
```

### Share output with naas


```python
naas.asset.add(csv_output)

#-> to remove your output, uncomment this line and execute the cell
# naas.asset.delete(csv_output)
```
