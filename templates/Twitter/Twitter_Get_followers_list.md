<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Twitter/Twitter_Get_followers_list.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Twitter+-+Get+followers+list:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #twitter #api #followers #list #get #developer

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will demonstrate how to get a list of followers from Twitter using the API. This feature is only available on paid plan.

**References:**
- [Twitter API Documentation](https://developer.twitter.com/en/docs/twitter-api/users/follows/quick-start/follows-lookup)
- [Twitter API Authentication](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens)

## Input

### Import libraries


```python
import naas
import tweepy
from tweepy import Stream
import json
import pandas as pd
```

### Setup Variables
- `API_KEY`: [Twitter API Key](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens)
- `API_SECRET`: [Twitter API Secret](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens)
- `AUTH_TOKEN`: [Twitter Auth Token](https://developer.twitter.com/en/docs/authentication/oauth-2-0/application-only)
- `AUTH_SECRET`: [Twitter Auth Secret](https://developer.twitter.com/en/docs/authentication/oauth-2-0/application-only)
- `USER_ID`: Any preferred twitter user ID


```python
API_KEY = naas.secret.get("TWITTER_API_KEY")
API_SECRET = naas.secret.get("TWITTER_API_SECRET")
AUTH_TOKEN = naas.secret.get("TWITTER_AUTH_TOKEN")
AUTH_SECRET = naas.secret.get("TWITTER_AUTH_SECRET")
USER_ID = "JupyterNaas"
```

## Model

### Create the connection with Tweepy and TwitterAPI


```python
try:
    auth = tweepy.OAuthHandler(API_KEY, API_SECRET)
    auth.set_access_token(AUTH_TOKEN, AUTH_SECRET)
    api = tweepy.API(auth, wait_on_rate_limit = True)
    print("Connection creation successful...")
except:
    print("Connection creation failed...")
```

### Get followers list

This function will use the Twitter API to get a list of followers for a given user ID.


```python
def get_followers_list(username):
    followers_scraped = []
    user = api.get_user(screen_name = username)
    for i, _id in enumerate(tweepy.Cursor(api.followers_ids, screen_name=username).items()):
        print(i, _id)
        followers_scraped.append(_id)
    return followers_scraped
```

## Output

### Display result


```python
followers_list_id = get_followers_list(USER_ID)
print(followers_list_id)
```

### Save the result in a dataframe


```python
followers_list_name = []
for i in range(len(followers_list_id)):
    followers_list_name.append(api.get_user(followers_list_id[i]).screen_name)
    
df = pd.DataFrame(followers_list_name, columns=['Followers'])
print(df.head())
```
