---
description: Expose assets by url
---

# 🖼️ Assets

## Add

Copy in production this current file as asset \( file \) and allow to get it by calling the returned url `naas.asset.add()`

```python
naas.assets.add()
```

You will get url who download this current file when you open it.

![screenshot-add-asset](../.gitbook/assets/screenshot-2020-10-07-at-18.34.12.png)

### Other file

If you wanna ad other file than current one, give a path:

```python
naas.assets.add("path/to/my/super/data.csv")
```

### Parameters

`inline` : Get response in your web browser instead of downloading the result.

```python
params = {"inline": True}

naas.assets.add(params=params)
```

### Debug

```python
naas.assets.add(debug=True)
```

## List 

You can list all version of a file pushed into the production:

### Current file

```python
naas.assets.list()
```

### Other file 

```python
naas.assets.list(path="path/to/my/super/data.csv")
```

## Get 

You can get a version of a file pushed into the production:

### Get the last one

```python
naas.assets.get()
```

### With a file path

```python
naas.assets.get(path="path/to/my/super/data.csv")
```

### With history id

```python
naas.assets.get(histo="20201008101221879662")
```

### Combined

```python
naas.assets.get(path="path/to/my/super/data.csv", histo="20201008101221879662")
```

## Clear

You can clear previous version of a file pushed into the production:

### One

```python
naas.assets.clear(histo="20201008101221879662")
```

### Other Notebook

```python
naas.assets.clear(path="path/to/my/super/data.csv", histo="20201008101221879662")
```

### All

```python
naas.assets.clear()
```

### All for filepath

```python
naas.assets.clear(path="path/to/my/super/data.csv")
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path 

### Current

```python
naas.assets.delete()
```

### Other file

```python
naas.assets.delete(path="path/to/my/super/data.csv")
```

### Debug

```python
naas.assets.delete(debug=True)
```

## List Api

You don't remember how many Scheduled notebook you have ?

### Simple

```python
naas.assets.currents()
```

### Raw result 

```python
naas.assets.currents(raw=True)
```

