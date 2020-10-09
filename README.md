---
description: How to start using Naas in minutes.
---

# Get started

## Welcome to Naas

If you want to use Naas on your local Jupyter environment, it's free and open-source, just follow the procedure below  : 

{% page-ref page="local-install.md" %}

### Why Naas?

{% hint style="danger" %}
Jupyter Notebooks are awesome, but using them in production can be risky & messy.
{% endhint %}

{% hint style="success" %}
Naas allows any Jupyter Notebooks to become a safe production environment!
{% endhint %}

## First things first

Naas makes a dynamic production environment based out of your current folder.

Create a folder, open a notebook, and import Naas :

```python
import naas
```

### Schedule your first notebook

Send in production this notebook and run it, every day at 9:00 

```python
# do stuff in your notebook
naas.scheduler.add(recurrence="0 9 * * *")
```

{% page-ref page="features/scheduler.md" %}

### Add a Dependency

Send in production any file type like `test.csv` as a dependency:

```python
naas.dependency.add("test.csv")
```

{% page-ref page="features/dependency.md" %}

### Add a Secret key

Copy in production any secret key :

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

Remove the previous line and get your secret key with :

```python
naas.secret.get(name="MY_API_KEY")
```

This allow you to push your notebook in production without Sensitive data in it.

{% page-ref page="features/secret.md" %}

## Naas advanced

If you use Naas cloud they all work natively, otherwise go to :

{% page-ref page="onprem-install.md" %}

### Notebook as API

Copy in production this notebook and allow to run it by calling the returned url:

```python
naas.api.add()
```

Call the url with your navigator you will get a message and see the notebook has run.

If you want download the notebook result instead, add this line: 

```python
naas.api.respond_notebook()
```

{% page-ref page="features/api.md" %}

### Expose Asset

Copy in production this asset \( file \) and allow to get it by calling the returned url:

```python
link = naas.assets.add("tesla-chart.html")
```

{% page-ref page="features/asset.md" %}

### Notification

Send and email notification to anyone,  notify data have change, notebook have run etc.. 

```python
# Get link var from previous step
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : " + link
naas.notifications.send(email=email, subject=subject, content=content)
```

{% page-ref page="features/notification.md" %}





