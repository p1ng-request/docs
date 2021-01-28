---
description: 'Get data from uutside Naas network easily, usefull for OAuth and other stuff'
---

# 🔙 Callback \(Alpha\)

## Create

Create callback url 

```python
url, uuid = naas.callback.add()
```

## List 

You can list all callback  you have create

```python
df = naas.callback.list()
```

## Get 

You can get a callback result.

```python
data, headers = naas.callback.get(uuid)
```

### Wait until data present

```python
data, headers = naas.callback.get(uuid, True)
```

### Wait until data present with timeout

timeout is in seconds

```python
data, headers = naas.callback.get(uuid, True, 10)
```

### Get the full data

```python
data = naas.callback.get(uuid, raw=True)
```

## Delete

You can remove any callback by uuid. 

```python
naas.callback.delete(uuid)
```

## List all \(Admin\)

Allows retrieving the all callback made by all users as admin.

```python
import naas
naas.notifications.list_all()
```



