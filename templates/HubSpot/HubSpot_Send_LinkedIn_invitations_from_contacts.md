# Send LinkedIn invitations from contacts

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot\_Send\_LinkedIn\_invitations\_from\_contacts.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=HubSpot+-+Send+LinkedIn+invitations+from+contacts:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #hubspot #invitation #automation #sales #linkedin

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E\_TXYWitQkmwog/)

**Description:** This notebook send LinkedIn invitation to your HubSpot contacts.

### Input

#### Import libraries

```python
import naas
from naas_drivers import hubspot, linkedin
import pandas as pd
import os
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

# LinkedIn limit invitations up to 100 per week (Becareful !)
LIMIT = 15
```

#### Setup Variables

```python
# CSV to manage and remove profile already in your contact
csv_contact = "LINKEDIN_EXISTING_CONTACT.csv"

# CSV to manage URL not valid
csv_not_valid = "LINKEDIN_NOT_VALID.csv"

# CSV to store invitations sent
csv_invitation = "LINKEDIN_INVITATIONS_SENT.csv"
```

#### Setup Naas

```python
# Scheduler your invitation everyday at 8:00 AM
naas.scheduler.add(cron="30 9 * * *")

# Uncomment the line below to delete your scheduler
# naas.scheduler.delete()
```

### Model

#### Get contacts from HubSpot

```python
df_contacts = gsheet.connect(SPREADSHEET_URL).get(SHEET_NAME)
df_contacts
```

#### Filter dataframe (if needed)

```python
def filter_data(df):
    df = df
    return df.reset_index(drop=True)


df_hubspot = filter_data(df_contacts)
df_hubspot
```

#### Get LinkedIn invitations sent

```python
df_lk_invitations = linkedin.connect(LI_AT, JSESSIONID).invitation.get_sent()
df_lk_invitations
```

#### Get profile checked and already in your network

```python
def get_csv(output_path):
    df = pd.DataFrame()
    if os.path.exists(output_path):
        df = pd.read_csv(output_path).drop_duplicates()
    return df
```

```python
df_contacts = get_csv(csv_contact)
df_contacts
```

#### Get URL not valid

```python
df_not_valid = get_csv(csv_not_valid)
df_not_valid
```

#### Get invitations sent (CSV)

Public ID can be different between what we get from LinkedIn and from your source URL.\
So we need to double check invitations sent with a CSV stored on your local

```python
df_csv_invitations = get_csv(csv_invitation)
df_csv_invitations
```

#### Get new invitation

* Clean Notion database to get valid URL
* Remove profile when already invited

```python
def get_new_invitations(
    df_hubspot, df_lk_invitations, df_csv_invitations, df_contacts, df_not_valid
):
    # Cleaning
    df = df_hubspot.copy()
    df["PROFILE_ID"] = df.apply(
        lambda row: row[col_linkedin].split("com/in/")[-1].split("/")[0], axis=1
    )
    print("✔️ LinkedIn valid URL :", len(df))

    # Get list of pending LinkedIn invitations
    pending_lk_invitations = []
    if len(df_lk_invitations) > 0:
        pending_lk_invitations = df_lk_invitations["PUBLIC_ID"].unique().tolist()
    print("❌ Pending LinkedIn invitations :", len(pending_lk_invitations))

    # Get list of CSV invitations
    pending_csv_invitations = []
    if len(df_csv_invitations) > 0:
        pending_csv_invitations = df_csv_invitations["PUBLIC_ID"].unique().tolist()
    print("❌ Pending CSV invitations :", len(pending_csv_invitations))

    # Get profile already in network
    contacts = []
    if len(df_contacts) > 0:
        contacts = df_contacts["PUBLIC_ID"].unique().tolist()
    print("❌ Already in network :", len(contacts))

    # Get profile not valid
    not_valids = []
    if len(df_not_valid) > 0:
        not_valids = df_not_valid["PROFILE_ID"].unique().tolist()
    print("❌ Profile not valid:", len(not_valids))

    # Remove pending invitations / already in network / not valid profile from dataframe
    exclude = pending_lk_invitations + pending_csv_invitations + contacts + not_valids
    df = df[~df["PROFILE_ID"].isin(exclude)].reset_index(drop=True)
    print("➡️ New invitation:", len(df))
    return df


df_new_invitations = get_new_invitations(
    df_hubspot, df_lk_invitations, df_csv_invitations, df_contacts, df_not_valid
)
df_new_invitations
```

#### Send invitation

```python
def send_invitation(df, df_not_valid=None, df_contacts=None, df_csv_invitations=None):
    # Check if new invitations to perform
    if len(df) == 0:
        print("🤙 No new invitations to send")
        return df

    # Setup variables
    if df_not_valid is None:
        df_not_valid = pd.DataFrame()
    if df_contacts is None:
        df_contacts = pd.DataFrame()
    if df_csv_invitations is None:
        df_csv_invitations = pd.DataFrame()

    # Loop
    count = 1
    for index, row in df.iterrows():
        df_network = pd.DataFrame()
        profile = row[col_linkedin]
        print(f"➡️ Checking :", profile)

        # Get distance with profile
        try:
            df_network = linkedin.connect(LI_AT, JSESSIONID).profile.get_network(
                profile
            )
        except Exception as e:
            # If error, profile URL is not valid => append Notion page to CSV not valid to not check it again
            df_not_valid = pd.concat([df_not_valid, df[index : index + 1]])
            df_not_valid.to_csv(csv_not_valid, index=False)
            print("❌ URL not valid", e)

        # Check if profile is already in your network
        if len(df_network) > 0:
            distance = df_network.loc[0, "DISTANCE"]
            # If not profile in network...
            if distance not in ["SELF", "DISTANCE_1"]:
                # => send invitation
                try:
                    linkedin.connect(LI_AT, JSESSIONID).invitation.send(
                        recipient_url=profile
                    )
                    print(count, "- 🙌 Invitation successfully sent")
                    df_csv_invitations = pd.concat([df_csv_invitations, df_network])
                    df_csv_invitations.to_csv(csv_invitation, index=False)
                except Exception as e:
                    print("❌ Invitation not sent", e)
                count += 1
            else:
                # If profile already in your network => append network result to CSV existing contact to not check it again
                df_contacts = pd.concat([df_contacts, df_network])
                df_contacts.to_csv(csv_contact, index=False)
                print(f"👍 Already in my network, 💾 saved in CSV")

        # Manage LinkedIn limit
        if count > LIMIT:
            print("⚠️ LinkedIn invitation limit reached", LIMIT)
            return df_csv_invitations
    return df_csv_invitations


df_csv_invitations = send_invitation(
    df_new_invitations, df_not_valid, df_contacts, df_csv_invitations
)
```

### Output

#### Send CSV as dependencies

```python
if os.path.exists(csv_contact):
    naas.dependency.add(csv_contact)

if os.path.exists(csv_not_valid):
    naas.dependency.add(csv_not_valid)

if os.path.exists(csv_invitation):
    naas.dependency.add(csv_invitation)
```

#### Display invitations sent

```python
df_csv_invitations
```
