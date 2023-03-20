<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Create_Post.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Create+Post:+Error+short+description">Bug report</a>

**Tags:** #linkedin #create #api #post #snippet 

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates a post using Linkedin API and Supabase.

**References:**
- [Linkedin API Documentation](https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/share-on-linkedin?context=linkedin%2Fconsumer%2Fcontext#create-a-text-share)
- [Supabase - Login with LinkedIn](https://supabase.com/docs/guides/auth/social-login/auth-linkedin)

## Input

### Import libraries


```python
import os
try:
    from supabase import create_client, Client
except:
    !pip install supabase --user
    from supabase import create_client, Client
import naas
import requests
import json
```

### Setup Variables
- [Supabase - Login with LinkedIn](https://supabase.com/docs/guides/auth/social-login/auth-linkedin)


```python
# Inputs
url = naas.secret.get("SUPABASE_URL") or "https://<project_id>.supabase.co"
key = naas.secret.get("SUPABASE_KEY") or "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imdxxxxxxxxxxxx" # Project API keys - https://app.supabase.com/project/<project_id>./settings/api

# Outputs
post_message = "Check out the LinkedIn Share API!"
```

### Connect to Supabase
- Click on the link to connect supabase to your LinkedIn account
- Copy/Paste the URL of the redirected page on the cell below


```python
supabase: Client = create_client(url, key)
data = supabase.auth.sign_in_with_oauth({
  "provider": 'linkedin',
  "options": {
      "scopes": 'w_member_social'
  }
})
print(data)
```

### Get your provider token


```python
url_lk = input('Copy/Paste your URL')
access_token = url_lk.split("provider_token=")[-1].split("&")[0]
access_token
```

## Model

### Get your user info


```python
headers = {
    "Authorization": f"Bearer {access_token}",
    "Content-Type": "application/json",
    "X-Restli-Protocol-Version": "2.0.0"
}

def user_info(headers):
    '''
    Get user information from Linkedin
    '''
    response = requests.get('https://api.linkedin.com/v2/me', headers=headers)
    print(response.json())
    user_info = response.json()
    return user_info
 
# Get user id to make a UGC post
user_info = user_info(headers)
urn = user_info['id']
urn
```

### Create Post with Image

Using the Linkedin Voyager API, we can create a post with an image. We need to set the `shareMediaCategory` to `IMAGE` and provide the `originalUrl` of the image.


```python
url = "https://api.linkedin.com/v2/ugcPosts"
data = {
    "author": f"urn:li:person:{urn}",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
        "com.linkedin.ugc.ShareContent": {
            "shareCommentary": {"text": post_message},
            "shareMediaCategory": "NONE"
        }
    },
    "visibility": {"com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC"}, #PUBLIC, CONNECTIONS
}
response = requests.post(url, headers=headers, data=json.dumps(data))
print(response.json())
```

## Output

### Display result


```python
from pprint import pprint
pprint(response.json())
```

 
