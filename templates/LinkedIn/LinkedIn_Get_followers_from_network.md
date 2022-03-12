# Get followers from network

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/open\_in\_naas.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_followers\_from\_network.ipynb)

**Tags:** #linkedin #network #followers #naas\_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

### Input

#### Import library

```python
from naas_drivers import linkedin
```

#### Get your cookies

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

### Model

Note : Due to follower privacy, it will not match with the exact number of followers.\


Get the information return in a dataframe.\
\
**Available columns :**

* PROFILE\_URN : LinkedIn unique profile id
* PROFILE\_ID : LinkedIn public profile id
* FIRSTNAME
* LASTNAME
* OCCUPATION
* FOLLOWER\_COUNT
* FOLLOWING
* FOLLOWING\_TYPE
* INFLUENCER

```python
df = linkedin.connect(LI_AT, JSESSIONID).network.get_followers(limit=-1)
```

### Output

#### Display result

```python
df
```
