# Get connections from network

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_connections\_from\_network.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+connections+from+network:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #network #connections #naas\_drivers #analytics #csv #html #image #content #plotly

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook helps you to build your professional network on LinkedIn by connecting with people in your network.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import pandas as pd
from datetime import datetime
import naas
import plotly.graph_objects as go
```

#### Setup LinkedIn

👉 [How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585
```

#### Variables

```python
# Outputs
title = "LinkedIn - Connections"
name_output = "LinkedIn_connections"
csv_output = f"{name_output}.csv"
html_output = f"{name_output}.html"
image_output = f"{name_output}.png"
```

### Model

#### Get connections from LinkedIn network

**Available columns :**

* FIRSTNAME : First name
* LASTNAME : Last name
* OCCUPATION : Text below the name in the profile page
* CREATED\_AT : Date of connection between and your connection
* PROFILE\_URL : Profile URL
* PROFILE\_PICTURE : Profile picture URL
* PROFILE\_ID : LinkedIn profile id
* PUBLIC\_ID : LinkedIn public profile id

```python
df_connections = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(limit=-1)
df_connections
```

### Output

#### Save connections to CSV

```python
df_connections.to_csv(csv_output, index=False)
```

#### Share outputs with naas

```python
naas.asset.add(csv_output)

# -> to remove your outputs, uncomment the lines and execute the cell
# naas.asset.delete(csv_output)
```
