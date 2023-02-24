<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Supabase/Supabase_Email_Auth.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Supabase+-+Email+Auth:+Error+short+description">Bug report</a>

**Tags:** #supabase #auth #email #signin #signout #verification

**Author:** [Sriniketh Jayasendil](http://linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will utilize the Supabase DB and Authentication (with email verification) to Login users.

**References:**
- [Supabase Signin](https://supabase.com/docs/reference/python/auth-signinwithpassword)

## Input

### Import libraries


```python
import naas
import json

try:
    from supabase import create_client
except ModuleNotFoundError:
    !pip install supabase --user
    from supabase import create_client
```

### Add naas secret


```python
# naas.secret.add(name="SUPABASE_URL", secret="")
# naas.secret.add(name="SUPABASE_KEY", secret="")
# naas.secret.add(name="USER_EMAIL", secret="")
# naas.secret.add(name="USER_PASSWORD", secret="")
```

### Setup Variables

First head to https://app.supabase.com/projects and create a new project. Then go to the `Project Setting\API` in the left panel. You could find the all these variables there. 

- `url`: A RESTful endpoint for querying and managing your database.
- `key`: Please use the public key
- `email`: Any valid email id
- `password`: A password of atleast 6 charachters
- `session`: To keep track of the login status of the particular user.


```python
# Inputs
url = naas.secret.get("SUPABASE_URL") or "SUPABASE_URL"
key = naas.secret.get("SUPABASE_KEY") or "SUPABASE_KEY"
email = naas.secret.get("USER_EMAIL") or "USER_EMAIL"
password = naas.secret.get("USER_PASSWORD") or "USER_PASSWORD"

# Outputs
session = ""
```

## Model

### Create the new supabase client


```python
Client = create_client(url, key)

# print(Client)
```

### Create new user 
Similar to sign up logic.

**Note:** After you run the query successfully you will get an verification email in the provided mail id.


```python
# To sign up user
res = Client.auth.sign_up({
  "email": email,
  "password": password,
})

# print(res)
```

### Login user

Use the credentials as you provided above


```python
# To login user
try:
    session = Client.auth.sign_in_with_password({
        "email": email,
        "password": password
    })
    print('Login successful...🚀')
    
except:
    print('Login failed!!!\n\n\nPotential reasons could be\n1. Make sure to confirm the email address.\n2. Check your spam incase if you are unable to find the email.\n3. If not the above ones check supabase docs: https://supabase.com/docs/reference/python/auth-signinwithpassword')
```

### To sign out user

Use the just the module without any parameters


```python
# To terminate the session / sign out the user
Client.auth.sign_out()
print('Logout successful👋...')
```

## Output

### Display result


```python
print(session)
```
