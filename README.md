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
Naas allows Jupyter Notebooks to become a safe production environment!
{% endhint %}

## Basic features

Naas makes a dynamic production environment based on your current notebook folder.

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

Send an email notification to anyone, to notify about data changes, alert on notebooks operations, etc...

```python
# Get link var from previous step
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : " + link
naas.notifications.send(email=email, subject=subject, content=content)
```

{% page-ref page="features/notification.md" %}

## Help

### Open

If at any time you are lost, you need help, or just want some info!

```python
import naas

naas.open_help()
```

That will open a chat box with us

### Close help chat

```python
import naas

naas.close_help()
```

## Best practices

After few months of using our own product and with the help of all of you we have found a set of practices that help to keep the Naas working your use cases!

Create a folder in your Naas by project, ideally, in this project, you should find:

* **Input** folder where you put every file you use as dependency to your notebook.
* **Output** folder ****where you save all results of your notebook, intermediary or final
* **Script** folder where you put your notebooks, all with a clear name of what they do.
* **deploy.ipynb** who is there to list and send all your sandbox files in production, it will prevent you to send your work in production by restarting a kernel!

Use **real Database** for storing purposes, CSVs are great but please use it as debug, not for storing every move from excel loses all its meaning! 

To do so, use our Mongo connector and a **free instance** from Mongo Atlas, you have **512MB** a good point to start  :

{% embed url="https://www.mongodb.com/pricing" %}





* Don't use emoji, space, or weird characters this will lead to errors just for a name, do you really what to find that the name \`$t0️⃣ck of W/-\ll $street.csv\` was causing your bug after 10 hours?
* Don't create your own scheduler within the scheduler, like schedule every minute a script to choose which action to do. It will create a ton of output file, max you file storage very fast and debug with be a crazy hell!
* Don't put password or sensitive information in your notebook, for many reason this is not the rigth place to store them,  use our secret system instead, it store them encoded on your machine, not perfect but much better !  





## Documentation

Show a button to quickly open this documentation from Jupyter

```python
import naas
naas.doc()
```

