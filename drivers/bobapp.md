---
description: Interact with toucan toco app
---

# 👷‍♂️ Bobapp

{% embed url="https://bobapp.ai/" %}

## Connect

{% hint style="danger" %}
You must Connect before any other methods
{% endhint %}

```python
api_key = "you can find it in your bobapp account"
naas_drivers.bobapp.connect(api_key)
```

## Me

### Get

Get my account

```python
data = naas_drivers.bobapp.me.get()
```

### Update

Update my account

```python
data = {"id": 1, ...}
naas_drivers.bobapp.users.update(data)
```

## Smarttable

### Connect

```python
database = "database"
collection = "collection"
sm = naas_drivers.bobapp.connect_smarttable(database, collection)
```

### Get all

#### Basic

```python
data = sm.get_all()
```

#### Get all

Get all object with search query

```python
search = "test"
data = sm.get_all(search)
```

#### Get all by page

Get all object by page

```python
limit = 10
skip = 20
data = sm.get_all(skip, limit)
```

### Get

Get one object by id

```python
id = "id"
data = sm.get(id)
```

### Send

Send one object

```python
data = {"id": 1, ...}
sm.insert(data)
```

### Update

Update one object

```python
data = {"id": 1, ...}
sm.update(data)
```

### Delete

Delete one object

```python
data = {"id": 1, ...}
sm.delete(data)
```

## Users

Only available if you are connected with admin account

### Create

```python
email = "bob@cashstory.com"
password = "test"
first_name = "bob"
last_name = "Cashstory"
role = "user"
workspace_id = "id"
workspace_name = "My workspace"
services = {}
naas_drivers.bobapp.users.create(
        email,
        password,
        first_name,
        last_name,
        role,
        workspace_id,
        workspace_name,
        services
)
```

### Create service

```python
service_name = "jupyter"
email = "bob@cashstory.com"
password = "test"
naas_drivers.bobapp.users.create_service(service_name, email, password)
```

### Update service

```python
service_name = "jupyter"
email = "bob@cashstory.com"
password = "test"
naas_drivers.bobapp.users.update_service(service_name, email, password)
```

### Update workspace

```python
email = "bob@cashstory.com"
workspace_id = "id"
workspace_name = "My workspace"
set_default = False
naas_drivers.bobapp.users.update_workspace(email, workspace_id, workspace_name, set_default)
```

### Create or Update

```python
email = "bob@cashstory.com"
password = "test"
first_name = "bob"
last_name = "Cashstory"
role = "user"
phone_number="+3000000",
user_role="CTO",
naas_drivers.bobapp.users.create_or_update(
    email, 
    password, 
    first_name,
    last_name,
    role,
    phone_number,
    user_role
    )
```

### Get by email

```python
email = "bob@cashstory.com"
user = naas_drivers.bobapp.users.get_by_email(email)
```

### Validate email

```python
email = "bob@cashstory.com"
naas_drivers.bobapp.users.validate_email(email)
```

### Get all

#### Basic

```python
data = naas_drivers.bobapp.users.get_all()
```

#### Get all

Get all user with search query

```python
search = "test"
data = naas_drivers.bobapp.users.get_all(search)
```

#### Get all by page

Get all user by page

```python
limit = 10
skip = 20
data = naas_drivers.bobapp.users.get_all(skip, limit)
```

### Get

Get one user by id

```python
id = "id"
data = naas_drivers.bobapp.users.get(id)
```

### Send

Send one user

```python
data = {"id": 1, ...}
naas_drivers.bobapp.users.insert(data)
```

### Update

Update one user

```python
data = {"id": 1, ...}
naas_drivers.bobapp.users.update(data)
```

### Delete

Delete one user

```python
data = {"id": 1, ...}
naas_drivers.bobapp.users.delete(data)
```

## Workspaces

Only available if you are connected with admin account

### Get all

#### Basic

```python
data = naas_drivers.bobapp.workspaces.get_all()
```

#### Get all

Get all workspace with search query

```python
search = "test"
data = naas_drivers.bobapp.workspaces.get_all(search)
```

#### Get all by page

Get all workspace by page

```python
limit = 10
skip = 20
data = naas_drivers.bobapp.workspaces.get_all(skip, limit)
```

### Get

Get one workspace by id

```python
id = "id"
data = naas_drivers.bobapp.workspaces.get(id)
```

### Send

Send one workspace

```python
data = {"id": 1, ...}
naas_drivers.bobapp.workspaces.insert(data)
```

### Update

Update one workspace

```python
data = {"id": 1, ...}
naas_drivers.bobapp.workspaces.update(data)
```

### Delete

Delete one workspace

```python
data = {"id": 1, ...}
naas_drivers.bobapp.workspaces.delete(data)
```



