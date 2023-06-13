<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_connections_from_network.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Get+connections+from+network:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #network #connections #naas_drivers #analytics #csv #html #image #content #plotly

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook helps you to build your professional network on LinkedIn by connecting with people in your network.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import libraries


```python
from naas_drivers import linkedin
import pandas as pd
from datetime import datetime
import naas
import plotly.graph_objects as go
```

### Setup LinkedIn
👉 <a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585
```

### Variables


```python
# Outputs
title = "LinkedIn - Connections"
name_output = "LinkedIn_connections"
csv_output = f"{name_output}.csv"
html_output = f"{name_output}.html"
image_output = f"{name_output}.png"
```

## Model

### Get connections from LinkedIn network
**Available columns :**
- FIRSTNAME : First name
- LASTNAME : Last name
- OCCUPATION : Text below the name in the profile page
- CREATED_AT : Date of connection between and your connection
- PROFILE_URL : Profile URL
- PROFILE_PICTURE : Profile picture URL
- PROFILE_ID : LinkedIn profile id
- PUBLIC_ID : LinkedIn public profile id


```python
df_connections = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(limit=-1)
df_connections
```

## Output

### Save connections to CSV


```python
df_connections.to_csv(csv_output, index=False)
```

### Share outputs with naas


```python
naas.asset.add(csv_output)

# -> to remove your outputs, uncomment the lines and execute the cell
# naas.asset.delete(csv_output)
```
