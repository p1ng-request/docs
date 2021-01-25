---
description: How to start using Naas in minutes.
---

# 🚀 Get started

## Welcome to Naas

If you want to use Naas on your local Jupyter environment, it's free and open-source, just follow the procedure below  : 

{% page-ref page="more-info/local-install.md" %}

### Why Naas?

{% hint style="danger" %}
Jupyter Notebooks are awesome, but using them in production can be risky & messy.
{% endhint %}

{% hint style="success" %}
Naas allows any Jupyter Notebooks to become a safe production environment!
{% endhint %}

## Basic features

Naas makes a dynamic production environment based out of your current notebook folder.

Create a folder, open a notebook, and import Naas :

```python
import naas
```

### Schedule your notebook

Send in production this notebook and run it, every day at 9:00 

```python
# do stuff in your notebook
naas.scheduler.add(recurrence="0 9 * * *")
```

{% page-ref page="features/scheduler.md" %}

### Add a dependency

Send in production any file type like `test.csv` as a dependency:

```python
naas.dependency.add("test.csv")
```

{% page-ref page="features/dependency.md" %}

### Add a secret key

Copy in production any secret key :

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

Remove the previous line and get your secret key with :

```python
naas.secret.get(name="MY_API_KEY")
```

This allows you to push your notebook in production without sensitive data getting exposed. 

{% page-ref page="features/secret.md" %}

## Advanced features

If you use Naas cloud they all work natively, otherwise go to :

### Use Notebooks as API

Copy in production this notebook and allow to run it by calling the returned URL:

```python
naas.api.add()
```

Call the URL with your navigator you will get a message and see the notebook has run.

If you want to download the notebook result instead, add this line: 

```python
naas.api.respond_notebook()
```

{% page-ref page="features/api.md" %}

### Expose assets

Copy in production this asset \( file \) and allow to get it by calling the returned url:

```python
link = naas.assets.add("tesla-chart.html")
```

{% page-ref page="features/asset.md" %}

### Send notifications

Send an email notification to anyone, notify about data changes, alert on notebooks operations, etc...

```python
# Get link var from previous step
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : " + link
naas.notifications.send(email=email, subject=subject, content=content)
```

{% page-ref page="features/notification.md" %}

## Version

### Get

the version number in your local machine

```python
import naas
naas.version()
```

### Are you at the last version

```python
import naas

naas.up_to_date()
```

### Get remote version

the last version number in Github

```python
import naas
naas.get_last_version()
```

## Update

If you need update it will restart your machine

```python
import naas
naas.auto_update()

```

## Documentation

Show a button to quick open this documentation from Jupyter

```python
import naas
naas.doc()
```

## Help

If at any time you are lost, you need help, or just want some info !

```python
import naas

naas.open_help()
```

## Changelog

Show changelog

```python
import naas
naas.changelog()
```

## Feature request

show feature request inside Jupyter

```python
import naas
mode = "naas" # can be naas, naas_drivers, awesome_notebook
naas.feature_request(mode)
```

## Check if you are in production

```python
import naas

naas.is_production()
```

