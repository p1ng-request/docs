---
description: Interact with Jupyter app
---

# 🪐 Jupyter

{% embed url="https://jupyter.org/hub" caption="Website" %}

## Connect

{% hint style="danger" %}
You must Connect before any other methods
{% endhint %}

You should get your token here :

{% hint style="success" %}
In Naas cloud you can connect without any argument it will find your token alone
{% endhint %}

{% embed url="https://app.naas.ai/hub/token" %}

```python
token = "*****"
jp = naas_drivers.jupyter.connect(token)
```

## Me

### Get 

```python
me = jp.get_me()
```

### Uptime

```python
uptime = jp.get_me_uptime()
```

## Admin

Only Naas admin can do it

### Users

```python
users = jp.get_users()
```

### User

```python
email = "bob@cashstory.com"
user = jp.get_user(email)
```

### Create

```python
email = "bob@cashstory.com"
password = "****"
user = jp.create_user(email, password)
```

### Get Authorize

Get one Authorization for user.

```python
email = "bob@cashstory.com"
is_authorize = jp.get_authorize_user(email)
```

### Authorize

Authorize one user.

```python
email = "bob@cashstory.com"
is_authorize = True
user = jp.change_authorize_user(email, is_authorize)
```

### Active

check if user has running server

```python
email = "bob@cashstory.com"
active = jp.is_user_active(email)
```

### Server uptime

```python
email = "bob@cashstory.com"
uptime = jp.get_server_uptime(email)
```

### Stop user

```python
email = "bob@cashstory.com"
jp.stop_user(email)
```

### Start user

```python
email = "bob@cashstory.com"
jp.start_user(email)
```

### Restart user

```python
email = "bob@cashstory.com"
jp.restart_user(email)
```

## Official documentation

{% embed url="https://jupyterhub.readthedocs.io/en/stable/reference/rest.html" %}

