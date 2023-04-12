<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Update_jobtitle_country_industry_from_linkedin.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Update+jobtitle+country+industry+from+linkedin:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #crm #sales #contact #naas_drivers #linkedin #identity #scheduler #naas #automation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook update the jobtitle, country and industry for a contact in HubSpot.

## Input

### Import libraries


```python
from naas_drivers import hubspot, linkedin
import naas
import pandas as pd
```

### Setup HubSpot
👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).


```python
# Enter Your Access Token
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

### Setup LinkedIn
If you are using the Chrome Extension:

- [Install Naas Chrome Extension](https://chrome.google.com/webstore/detail/naas/cpkgfedlkfiknjpkmhcglmjiefnechpp?hl=fr&authuser=0)
- [Create a new token](https://app.naas.ai/hub/token)
- Copy/Paste your token in your extension
- Login/Logout your LinkedIn account
- Your secrets "LINKEDIN_LI_AT" and "LINKEDIN_JSESSIONID" will be added directly on your naas everytime you login and logout.

or <br>

If you are not using the Google Chrome Extension, [learn how to get your cookies on LinkedIn](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75) and set up the values below:
- 🍪 li_at
- 🍪 JSESSIONID


```python
# Cookies
LI_AT = naas.secret.get("LINKEDIN_LI_AT") or "YOUR_COOKIE_LI_AT"
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID") or "YOUR_COOKIE_JSESSIONID"

# LinkedIn update limit
LIMIT = 15
```

### Setup Naas


```python
naas.scheduler.add(cron="0 8 * * *")

# -> Uncomment the line below (by removing the hashtag) to remove your scheduler
# naas.scheduler.delete()
```

## Model

### Get all contacts in Hubspot


```python
properties_list = [
    "hs_object_id",
    "firstname",
    "lastname",
    "linkedinbio",
    "jobtitle",
    "country",
    "industry",
]
hubspot_contacts = hubspot.connect(HS_ACCESS_TOKEN).contacts.get_all(properties_list)
hubspot_contacts
```

### Filter to get "jobtitle", "country", "industry" = "Not Defined" and "linkedinbio" = defined


```python
df_to_update = hubspot_contacts.copy()

# Cleaning
df_to_update = df_to_update.fillna("Not Defined")

# Filter on "Not defined"
df_to_update = df_to_update[
    (df_to_update.linkedinbio != "Not Defined")
    & (df_to_update.jobtitle == "Not Defined")
    & (df_to_update.country == "Not Defined")
    & (df_to_update.industry == "Not Defined")
]

# Limit to last x contacts
df_to_update = df_to_update.sort_values(by="createdate", ascending=False)[
    :LIMIT
].reset_index(drop=True)

df_to_update
```

### Get identity from Linkedin


```python
for _, row in df_to_update.iterrows():
    linkedinbio = row.linkedinbio

    # Get followers
    df = linkedin.connect(LI_AT, JSESSIONID).profile.get_identity(linkedinbio)
    jobtitle = df.loc[0, "OCCUPATION"]
    industry = df.loc[0, "INDUSTRY_NAME"]
    country = df.loc[0, "COUNTRY"]

    # Get linkedinbio
    df_to_update.loc[_, "jobtitle"] = jobtitle
    df_to_update.loc[_, "industry"] = industry
    df_to_update.loc[_, "country"] = country

df_to_update
```

## Output

### Update jobtitle, country, industry in Hubspot


```python
for _, row in df_to_update.iterrows():
    # Init data
    data = {}

    # Get data
    hs_object_id = row.hs_object_id
    jobtitle = row.jobtitle
    industry = row.industry
    country = row.country

    # Update
    if jobtitle != None:
        data = {
            "properties": {
                "jobtitle": jobtitle,
                "industry": industry,
                "country": country,
            }
        }
    hubspot.connect(HS_ACCESS_TOKEN).contacts.patch(hs_object_id, data)
```
