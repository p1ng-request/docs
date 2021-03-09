---
description: Expose assets by URL.
---

# 🖼️ Assets

## Add

Copy in production this current file as an asset \(file\) and allow yourself to get it by calling the returned URL.

```python
naas.assets.add()
```

You will get URL who downloads this current file when you open it.

![screenshot-add-asset](../.gitbook/assets/screenshot-2020-10-07-at-18.34.12.png)

### Other files

If you want to add another file than the current one, give a path:

```python
naas.assets.add("path/to/my/super/data.csv")
```

### Parameters

`inline` : Get a response in your web browser instead of downloading the result.

```python
params = {"inline": True}

naas.assets.add(params=params)
```

### Debug

```python
naas.assets.add(debug=True)
```

## Find

You can find url of a file pushed into the production:

### Current file

```python
url = naas.assets.find()
```

### Other files 

```python
url = naas.assets.find(path="path/to/my/super/notebook.ipynb")
```

## List 

You can list all version of a file pushed into the production:

### Current file

```python
naas.assets.list()
```

### Other files 

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

You can clear the previous version of a file pushed into the production:

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

You can remove any scheduler capability like that, it takes optionally a path.

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

## List Assets

You don't remember how many Assets notebook you have?

### Simple

```python
naas.assets.currents()
```

### Raw result 

```python
naas.assets.currents(raw=True)
```

