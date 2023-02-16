<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twitter/Twitter_Get_members_of%20list.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twitter+-+Get+members+of+list:+Error+short+description">Bug report</a>

**Tags:** #twitter #tweepy #pandas #twitterautomation #twitterlistmembers #snippet

**Author:** [Kaushal Krishna](https://www.linkedin.com/in/kaushal-krishna-a48959153)

**Description:** This notebook gets the members of a list of a particular user. Private list members will only be shown if the authenticated user owns the specified list. It can be used to enable people to curate and organize new Lists based on the membership information

<u>References:</u>
- https://developer.twitter.com/en/docs/twitter-api/lists/list-members/introduction

## Input

### Import libraries


```python
import tweepy
import pandas as pd
import naas
```

### Setup Variables
-> Get your bearer token by applying in twitter developer website https://developer.twitter.com/en/docs/authentication/oauth-2-0/bearer-tokens            
-> For the user name supply the display name (Twitter Handle) without '@' i.e.  "JupyterNaas" for Naas.ai .                                                                                                                                                                                      
-> The list has to be public in order to be noticed by the api.


```python
# inputs
bearer_token = (
    naas.secret.get("TWITTER_BEARER_TOKEN")
    or "AAAAAAAAAAAAAAAAAAAAAMQhdgEAAAAAD0EI4sREei02us..."
)
user_name = "JupyterNaas"

# outputs
csv_output = "output.csv"
```

## Model

### Connect to client


```python
try:
    client = tweepy.Client(bearer_token=bearer_token)
except:
    print("Failure in Authentication.")
```

### Get data from Twitter


```python
def get_members_of_list(client, user_name):
    user = client.get_user(username=user_name)
    user_id = user.data["id"]
    twitter_list = client.get_owned_lists(id=user_id)

    # init result
    data_dict = {
        "LIST_ID": [],
        "LIST_NAME": [],
        "MEMBER_ID": [],
        "MEMBER_NAME": [],
        "MEMBER_USERNAME": [],
    }

    for row in twitter_list.data:
        list_id = row["id"]
        list_name = row["name"]
        list_members = client.get_list_members(id=list_id)
        for member in list_members.data:
            data_dict["LIST_ID"].append(list_id)
            data_dict["LIST_NAME"].append(list_name)
            data_dict["MEMBER_ID"].append(member["id"])
            data_dict["MEMBER_NAME"].append(member["name"])
            data_dict["MEMBER_USERNAME"].append(member["username"])
    df = pd.DataFrame(data_dict)
    return df


df_members = get_members_of_list(client, user_name)
df_members
```

## Output

### Save result in csv


```python
df.to_csv(csv_output, index=False)
```
