---
description: Link custom domain to your public url
---

# 🏰Domain

## Simple

Copy in production this notebook as a dependency and allow notebooks to use it. 

```python
url = "https://public.naas.ai/****/asset/****"
naas.domain.add("google.com", url)
```

## Status

Check status of domain service

```python
status = naas.domain.status()
```

## Global Add

```python
naas.domain.add("google.com", url)
```

## Get all

Check list of all my register domain

```python
domains = naas.domain.get()
```

## Delete simple

```python
url = "https://public.naas.ai/****/asset/****"
naas.domain.delete("google.com", url)
```

## Delete global

```python
naas.domain.delete("google.com")
```

