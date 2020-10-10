---
description: Copy in secure location your sensible data and allow Notebook to use it.
---

# 🔑 Secret keys

## Simple

Copy in production your secret keys and allow notebooks to use it. 

### Add

Name your secret and add it's key.

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

{% hint style="info" %}
You can delete this line from your notebook after running it, your data is safe and secure.
{% endhint %}

### Get

Returns your secret \(use with caution\).

```python
naas.secret.get(name="MY_API_KEY")
```

## List current

You don't remember how many secrets you have?

```python
naas.secret.currents()
```

Optionally you can get the raw result :

```python
naas.secret.currents(raw=True)
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path.

```python
naas.secret.delete()
```

## Debug

Need to understand why something goes bad?

```python
naas.secret.add("test.csv", debug=True)
# or
naas.secret.delete("test.csv", debug=True)
```



