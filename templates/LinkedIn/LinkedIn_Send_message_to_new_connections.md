# Send message to new connections

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Send\_message\_to\_new\_connections.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Send+message+to+new+connections:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #message #naas\_drivers #content #snippet #text

**Author:** [Asif Syed](https://www.linkedin.com/in/www.linkedin.com/in/asifsyd/)

**Description:** This notebook allows users to quickly and easily send messages to their new LinkedIn connections.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import pandas as pd
from datetime import date
import naas
```

#### Setup LinkedIn

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = (
    naas.secret.get("LI_AT") or "ENTER_YOUR_COOKIE_LI_AT_HERE"
)  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = (
    naas.secret.get("JSESSIONID") or "ENTER_YOUR_COOKIE_JSESSIONID_HERE"
)  # EXAMPLE ajax:8379907400220387585
```

#### Setup custom message

The message format sent to new connections is structured as follows - Greeting{space}First\_Name{comma}{space}Message

eg: Hi Asif, thank you for connecting with me!

First\_Name is directly fetched from the dataframe and we can customize the Greeting and Message parameters by editing the strings in the below cell.

```python
Greeting = "Hi"
Message = "Thank you for connecting with me!"
```

### Model

#### Get last connections

Get the recent connections data (limit parameter can be changed as per your requirement; it is the maximum number of new connections to whom you want to send the message)

```python
df = linkedin.connect(LI_AT, JSESSIONID).network.get_connections(limit=100)
df.head(5)
```

#### Filter data

```python
def filter_data(df):
    df["CREATED_AT"] = pd.to_datetime(
        df["CREATED_AT"]
    ).dt.date  # changing the CREATED_AT column data to datetime format
    df = df[
        df["CREATED_AT"] == date.today()
    ]  # restricting the dataframe to hold only the details of people connected today
    return df


df_profiles = filter_data(df)
print("✅ New connections today:", len(df_profiles))
df_profiles
```

### Output

#### Send the message

```python
for (
    index,
    row,
) in (
    df_profiles.iterrows()
):  # looping through each profile in the dataframe of new connections
    firstname = row["FIRSTNAME"]
    lastname = row["LASTNAME"]
    profile_url = row["PROFILE_URL"]
    result = linkedin.message.send(
        content=Greeting + " " + firstname + "," + " " + Message,
        recipients_url=profile_url,
    )
    print(f"✅ Message sent to {firstname} {lastname}")
```
