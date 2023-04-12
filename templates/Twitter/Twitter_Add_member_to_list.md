    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twitter/Twitter_Add_member_to_list.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twitter+-+Add+member+to+list:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #twitter #tweepy #pandas #twitterautomation #twitterlistmembers #snippet

**Author:** [Kaushal Krishna](https://www.linkedin.com/in/kaushal-krishna-a48959153)

**Description:** This notebook adds a member to the list of a particular user.

## Input

### Import libraries


```python
import tweepy
import pandas as pd
import naas
```

### Setup Variables
-> Get your bearer token by applying in twitter developer website https://developer.twitter.com/en/docs/authentication/oauth-2-0/bearer-tokens  
-> Get your Oauth 1.0 token by applying into twitter developer website with Read and Write Permission https://developer.twitter.com/en/docs/authentication/oauth-1-0a     
-> For the user name supply the display name (Twitter Handle) without '@' i.e.  "JupyterNaas" for Naas.ai    
-> Please consult the tweepy docs for more help on authentication https://docs.tweepy.org/en/stable/authentication.html

**The bearer_token is for Oauth 2.0 user lookup and consumer_key, consumer_secret ,access_token, access_token_secret are for Oauth 1.0 get_user(by username parameter) list lookup(even private ones),list_member lookup  list add member and remove member**


```python
# inputs
tw_bearer_token = (
    naas.secret.get("TWITTER_BEARER_TOKEN")
    or "AAAAAAAAAAAAAAAAAAAAAMQhdgEAAAAAGxxxJUpXgWUPS%2Bzf36a8OPmBzo%3DebY7xxxxxxxxxxxxxxxxxxxxxxx"
)
tw_consumer_key = (
    naas.secret.get("TWITTER_CONSUMER_KEY") or "Tms4ZxxvvJiHYGo8Gxxxxxxxxxx"
)
tw_consumer_secret = (
    naas.secret.get("TWITTER_CONSUMER_SECRET")
    or "aDQgJ8pGxxxGTxBa4i5gx7BKYE4UzFZ7xxxxxxxx"
)
tw_access_token = (
    naas.secret.get("TWITTER_ACCESS_TOKEN")
    or "1328105689898766336-9OZis7LOnljJakLRQxxxxxxxxi"
)
tw_access_token_secret = (
    naas.secret.get("TWITTER_ACCESS_TOKEN_SECRET")
    or "eLIfxxxxxxx5xPBbc9l7Jk0QcqxxxxxxxxxxxZ9C"
)
user_name = "JupyterNaas"
list_name = "Cool Tweets"
member_username = "ravenel_jeremy"

# outputs
csv_output = "output.csv"
```

## Model

### Connect to client


```python
try:
    client_1 = tweepy.Client(bearer_token=tw_bearer_token)
    client_2 = tweepy.Client(
        consumer_key=tw_consumer_key,
        consumer_secret=tw_consumer_secret,
        access_token=tw_access_token,
        access_token_secret=tw_access_token_secret,
    )
except:
    print("Failure in Authentication.")
```

### Get list ID


```python
def find_list_id(list_name, user_name, client, user_auth=True):
    list_id = None
    user = client.get_user(username=user_name, user_auth=user_auth)
    user_id = user.data["id"]
    twitter_list = client.get_owned_lists(id=user_id, user_auth=user_auth)
    for row in twitter_list.data:
        if row["name"] == list_name:
            list_id = row["id"]
            break
    return list_id


list_id = find_list_id(list_name=list_name, user_name=user_name, client=client_2)
print(f"'{list_name}' ID:", list_id)
```

### Get member ID


```python
member_id = client_1.get_user(username=member_username).data["id"]
print(f"'{member_username}' ID:", member_id)
```

### Add list member


```python
res = client_2.add_list_member(id=list_id, user_id=member_id, user_auth=True)
res
```

## Output

### Get members from list


```python
def get_members_of_list(client, print_choice=False):
    user = client.get_user(username=user_name)
    user_id = user.data["id"]
    twitter_list = client.get_owned_lists(id=user_id)
    data_dict = {"Username": [], "Name": []}
    for row in twitter_list.data:
        list_id = row["id"]
        list_members = client.get_list_members(id=list_id)
        for member in list_members.data:
            data_dict["Username"].append(member["username"])
            data_dict["Name"].append(member["name"])
            if print_choice:
                print(
                    f"Username : {member['username']:<14} ||  Name : {member['name']:<28}"
                )
    return data_dict


dicter = get_members_of_list(client_1)
res_df = pd.DataFrame(dicter)
res_df
```

### Save result in csv


```python
res_df.to_csv(csv_output, index=False)
```
