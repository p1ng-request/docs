---
description: Add in production folder file needed by your notebooks
---

# 🔗 Dependency

## Simple

Copy in production this notebook as dependency and allow notebooksI to use it. 

```python
naas.dependency.add("test.csv")
```

### Debug

```python
naas.dependency.add(debug=True)
```

## List 

You can list all version of a file pushed into the production:

### Current file

```python
naas.dependency.list()
```

### Other file 

```python
naas.dependency.list(path="path/to/my/super/data.csv")
```

## Get 

You can get a version of a file pushed into the production:

### Get the last one

```python
naas.dependency.get()
```

### With a file path

```python
naas.dependency.get(path="path/to/my/super/data.csv")
```

### With history id

```python
naas.dependency.get(histo="20201008101221879662")
```

### Combined

```python
naas.dependency.get(path="path/to/my/super/data.csv", histo="20201008101221879662")
```

## Clear

You can clear previous version of a file pushed into the production:

### One

```python
naas.dependency.clear(histo="20201008101221879662")
```

### Other Notebook

```python
naas.dependency.clear(path="path/to/my/super/data.csv", histo="20201008101221879662")
```

### All

```python
naas.dependency.clear()
```

### All for filepath

```python
naas.dependency.clear(path="path/to/my/super/data.csv")
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path 

### Current

```python
naas.dependency.delete()
```

### Other file

```python
naas.dependency.delete(path="path/to/my/super/data.csv")
```

### Debug

```python
naas.dependency.delete(debug=True)
```

## List Api

You don't remember how many Scheduled notebook you have ?

### Simple

```python
naas.dependency.currents()
```

### Raw result 

```python
naas.dependency.currents(raw=True)
```



