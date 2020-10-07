---
description: Add in production folder file needed by your notebooks
---

# Dependency

## Simple

Copy in production this notebook as dependency and allow notebooksI to use it. 

```python
naas.dependency.add("test.csv")
```

## List current

You don't remember how many assets you have ?

```python
naas.dependency.currents()
```

Optionally you can get the raw result :

```python
naas.dependency.currents(raw=True)
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path .

```python
naas.dependency.delete()
```

## Debug

Need to understand why, something go bad ?

```python
naas.dependency.add("test.csv", debug=True)
# or
naas.dependency.delete("test.csv", debug=True)
```



