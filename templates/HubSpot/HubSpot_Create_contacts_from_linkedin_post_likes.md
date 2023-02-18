# Create contacts from linkedin post likes

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/open\_in\_naas.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot\_Create\_contacts\_from\_linkedin\_post\_likes.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=HubSpot+-+Create+contacts+from+linkedin+post+likes:+Error+short+description)

**Tags:** #hubspot #crm #sales #contact #naas\_drivers #linkedin #post #contact #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook create new contacts based on LinkedIn post likes.

### Input

#### Import librairies

```python
from naas_drivers import linkedin, hubspot
import naas
import requests
```

#### Setup HubSpot

👉 Starting November 30, 2022, HubSpot API keys no longer enable access to HubSpot APIs, so in Naas version 2.8.3 and above, you need [create a private app and use the access token](https://developers.hubspot.com/docs/api/private-apps).

```python
# Enter Your Access Token
HS_ACCESS_TOKEN = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

#### Setup LinkedIn

If you are using the Chrome Extension:

* [Install Naas Chrome Extension](https://chrome.google.com/webstore/detail/naas/cpkgfedlkfiknjpkmhcglmjiefnechpp?hl=fr\&authuser=0)
* [Create a new token](https://app.naas.ai/hub/token)
* Copy/Paste your token in your extension
* Login/Logout your LinkedIn account
* Your secrets "LINKEDIN\_LI\_AT" and "LINKEDIN\_JSESSIONID" will be added directly on your naas everytime you login and logout.

or\


If you are not using the Google Chrome Extension, [learn how to get your cookies on LinkedIn](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75) and set up the values below:

* 🍪 li\_at
* 🍪 JSESSIONID

```python
# Cookies
LI_AT = naas.secret.get("LINKEDIN_LI_AT") or "YOUR_COOKIE_LI_AT"
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID") or "YOUR_COOKIE_JSESSIONID"

# Post URL
POST_URL = "----"
```

### Model

#### Get post likes

```python
df_posts = linkedin.connect(LI_AT, JSESSIONID).post.get_likes(POST_URL)

# Display the number of likes
print("Number of likes: ", df_posts.PROFILE_URN.count())
```

```python
# Show dataframe with list of profiles from likes
df_posts
```

#### Create contacts from LinkedIn post likes

```python
def create_contacts_from_post(
    df,
    c_profile_urn="PROFILE_URN",
    c_firstname="FIRSTNAME",
    c_lastname="LASTNAME",
    c_occupation="OCCUPATION",
):
    for _, row in df.iterrows():
        profile_urn = row[c_profile_urn]
        firstname = row[c_firstname]
        lastname = row[c_lastname]
        occupation = row[c_occupation]
        linkedinbio = f"https://www.linkedin.com/in/{profile_urn}"
        email = None
        phone = None

        # contact
        try:
            contact = linkedin.connect(LI_AT, JSESSIONID).profile.get_contact(
                linkedinbio
            )
            email = contact.loc[0, "EMAIL"]
            phone = contact.loc[0, "PHONENUMBER"]
        except:
            print("No contact info")

        # With send method
        data = {
            "properties": {
                "linkedinbio": linkedinbio,
                "firstname": firstname,
                "lastname": lastname,
                "jobtitle": occupation,
                "email": email,
                "phone": phone,
            }
        }
        print(data)
        hubspot.connect(HS_ACCESS_TOKEN).contacts.send(data)
```

### Output

#### Display result

```python
create_contacts_from_post(df_posts)
```
