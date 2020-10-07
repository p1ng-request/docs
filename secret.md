---
description: Copy in secure location your sensible data and allow Notebook to use it.
---

# Secret

## Simple

Copy in production this notebook as dependency and allow notebooksI to use it. 

### Save it

```python
naas.secret.add(name="MY_API_KEY", secret="SUPER_SECRET_API_KEY")
```

{% hint style="info" %}
You can delete this line from your notebook after runned it, your data is saved and secure
{% endhint %}

### Get it 

```python
naas.secret.get(name="MY_API_KEY")
```

## List current

You don't remember how many assets you have ?

```python
naas.secret.currents()
```

Optionally you can get the raw result :

```python
naas.secret.currents(raw=True)
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path .

```python
naas.secret.delete()
```

## Debug

Need to understand why, something go bad ?

```python
naas.secret.add("test.csv", debug=True)
# or
naas.secret.delete("test.csv", debug=True)
```



