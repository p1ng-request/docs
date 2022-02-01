---
description: Link custom domain to your public url
---

# 🏰 Domain (Alpha)

If you are in our cloud&#x20;

{% hint style="danger" %}
This feature is in early-stage development!&#x20;

Contact devops@cashstory.com  to be able to test it.
{% endhint %}

{% hint style="info" %}
Set CNAME in your domain or subdomain to: ``&#x20;

abc046369c2ca408fb4e0e33cb35d006-b0f052c2a8fe9e46.elb.eu-west-3.amazonaws.com
{% endhint %}

## Simple

Copy in production this notebook as a dependency and allow notebooks to use it.&#x20;

```python
url = "https://public.naas.ai/****/asset/****"
naas.domain.add("google.com", url)
```

## Status

Check the status of domain service

```python
status = naas.domain.status()
```

## Global Add

```python
naas.domain.add("google.com", url)
```

## Get all

Get list of all my registered domain

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
