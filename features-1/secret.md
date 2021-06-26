---
description: Copy in secure location your sensible data and use it in your notebook.
---

# 🔑 Secret key

Secrets are an important part of Naas, when you need to interact with other services, you need secret, like any other variable the temptation is big to put it straight in your notebook, but this lead to a big security breach since we replicate a lot the notebook, in the versioning system, the output and your ability to share it or send it to git!  

Use this simple feature instead to have global secure storage share with your sandbox and production.

Secrets are local to your machine and encoded, that a big layer of security with a little effort.

## Add or edit secret

Add a new secret to your Naas

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

{% hint style="warning" %}
After running it, your data is safe and secure you can delete this line from your notebook.
{% endhint %}

To edit a secret, use the function above with the same name and change the secret parameters.

## Get your secret

Returns your secret store in Naas

```python
naas.secret.get(name="MY_API_KEY")
```

## List all secrets name's

You don't remember your secret?

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

