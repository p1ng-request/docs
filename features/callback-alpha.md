---
description: 'Get data from uutside Naas network easily, usefull for OAuth and other stuff'
---

# 🔙 Callback \(Alpha\)

## Create

Create callback url 

```python
url, uuid = naas.callback.add()
```

### Create without self destroy

```python
url, uuid = naas.callback.add(autoDelete=False)
```

### Create with custom response

```python
url, uuid = naas.callback.add(response={"toto": "tata"})
```

### Create with custom response headers

```python
url, uuid = naas.callback.add(responseHeaders={"toto": "tata"})
```

## List 

You can list all callback  you have create

```python
df = naas.callback.list()
```

## Get 

You can get a callback result.

if callback didn't been call yet, result will be `None`

```python
data, headers = naas.callback.get(uuid)
```

### Wait until data present 

{% hint style="info" %}
It will wait maximum 3000 sec
{% endhint %}

```python
data, headers = naas.callback.get(uuid, True)
```

### Wait until data present with Timeout

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



