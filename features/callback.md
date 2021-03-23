---
description: >-
  Get and receive data from outside Naas network, usefull for OAuth and other
  need who need light and fast response.
---

# 👈 Callback

## Create

Create callback URL 

```python
url, uuid = naas.callback.add()
```

###  Without self destroy

```python
url, uuid = naas.callback.add(auto_delete=False)
```

### With custom response

```python
url, uuid = naas.callback.add(response={"toto": "tata"})
```

### With custom response headers

```python
url, uuid = naas.callback.add(response_headers={"toto": "tata"})
```

### With default result

```python
url, uuid = naas.callback.add(default_result={"toto": "tata"})
```

### Disable override response

If URL is called multiple time, only the first response will be kept

```python
url, uuid = naas.callback.add(no_override=True)
```

### For specifics user \(Admin\)

```python
url, uuid = naas.callback.add(user="bob@cashstory.com")
```

### Force UUID \(Admin\)

```python
url, uuid = naas.callback.add(user="bob@cashstory.com", uuid="test")
```

## List 

You can list all callback  you have created

```python
df = naas.callback.list()
```

### For specifics user \(Admin\)

```python
url, uuid = naas.callback.list(user="bob@cashstory.com")
```

## Get 

You can get a callback result.

if a callback didn't been called yet, the result will be `None`

```python
data, headers = naas.callback.get(uuid)
```

### Wait until data present 

{% hint style="info" %}
It will wait a maximum of 3000 sec
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

### For specifics user \(Admin\)

```python
url, uuid = naas.callback.get(uuid, user="bob@cashstory.com")
```

## Delete

You can remove any callback by UUID. 

```python
naas.callback.delete(uuid)
```

### For specifics user \(Admin\)

```python
naas.callback.delete(user="bob@cashstory.com")
```

## List all \(Admin\)

Allows retrieving all callback made by all users as admin.

```python
import naas
naas.callback.list_all()
```



