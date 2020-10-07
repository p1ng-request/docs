---
description: get more option in asset
---

# Asset

## Basic add

Copy in production this current file as asset \( file \) and allow to get it by calling the returned url `naas.asset.add()`

```python
naas.assets.add()
```

You will get url who download this current file when you open it.

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



