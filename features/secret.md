---
description: Copy in secure location your sensible data and use it in your notebook.
---

# 🔑 Secret keys

## Add or edit secret

Add new secret in your naas

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

{% hint style="warning" %}
After running it, your data is safe and secure you can delete this line from your notebook.
{% endhint %}

To edit a secret, use the function above with the same name and change the secret parameters.

## Get your secret

Returns your secret store in naas

```python
naas.secret.get(name="MY_API_KEY")
```

## List all secrets name's

You don't remember your secret ?

```python
naas.secret.list()
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

