<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# LinkedIn - Linkedin Get info from company
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/Linkedin_Get_info_from_company.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #company #info #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import librairy


```python
from naas_drivers import linkedin
```

### Get your cookies
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

### Enter company URL, linkedin name or id


```python
COMPANY = "https://www.linkedin.com/company/tesla" #or universal name = "tesla" or id = "8819091"
```

## Model

Get the information return in a dataframe.<br><br>
**Available columns :**
- COMPANY_URN : LinkedIn unique id
- COMPANY_URL : LinkedIn public url
- COMPANY_NAME : Company name displayed
- UNIVERSAL_NAME
- WEBSITE
- DESCRIPTION
- COUNTRY
- REGION
- CITY
- STAFF_COUNT
- FOLLOWER_COUNT
- INDUSTRY


```python
df = linkedin.connect(LI_AT, JSESSIONID).company.get_info(COMPANY)
```

## Output

### Display result


```python
df
```
