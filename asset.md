---
description: Expose assets by url
---

# Asset

## Simple

Copy in production this current file as asset \( file \) and allow to get it by calling the returned url `naas.asset.add()`

```python
naas.assets.add()
```

You will get url who download this current file when you open it.

![screenshot-add-asset](.gitbook/assets/screenshot-2020-10-07-at-18.34.12.png)

## Other file

If you wanna ad other file than current one, give a path:

```python
naas.assets.add("text.csv")
```

## Inline

This will display from the url the file instead of download it .

```python
naas.assets.add(None, {"inline": True})
```

## List current

You don't remember how many assets you have ?

```python
naas.asset.currents()
```

Optionally you can get the raw result :

```python
naas.asset.currents(raw=True)
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path .

```python
naas.asset.delete()
```

## Debug

Need to understand why, something go bad ?

```python
naas.asset.add(debug=True)
# or
naas.asset.delete(debug=True)
```

