---
description: The open platform for data science creators and consumers.
cover: >-
  https://images.unsplash.com/photo-1506318137071-a8e063b4bec0?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw1fHxzdGFyc3xlbnwwfHx8fDE2NDM3MDc0ODE&ixlib=rb-1.2.1&q=85
coverY: 0
---

# Welcome to Naas

![](<.gitbook/assets/Untitled Design (1).jpg>)

{% hint style="warning" %}
This documentation is in `beta`. It may change frequently. To propose changes or enhancements, please create a [GitHub Issue.](https://github.com/jupyter-naas/docs)&#x20;
{% endhint %}

## **Why Naas?**

The ability to access live business insights from data provides a real competitive advantage.

Organizations collect a growing quantity of data across domains but only a few manage to connect the dots and extract the essential business value. This; is the purpose of data science.

The main problem is that the data often sits in different silos. This situation generates :

* Poor audibility
* Complex multi-channel distribution (email, chat, files, reports, social media)
* Lack of accountability

### **Naas is solving that with low-code.**

In the past decade, the low-code and no-code solutions have become a multi-billion dollar industry. The promise of these solutions is that anyone can build applications and automation using templates. Yet, no standard has emerged in “low-code data science”.

Naas was built to become this standard, comforted by Netflix publications explaining why they are investing in a Jupyter Notebook infrastructure to solve their data challenges.

### **Naas and Jupyter Notebooks.**

Naas leverages Jupyter Notebooks and its 10 million users. Jupyter Notebook is a web-based interactive computing platform for data science. A notebook is a document made with cells of live code, text and visualizations for data exploration, collaboration and storytelling.

Thanks to Naas low-code formulas, notebooks become more readable, more accessible, and interconnected to support faster business decision-making.

Naas augments Jupyter Notebooks by adding micro-services accessible in low-code to easily access data, automation, and AI.

![](<.gitbook/assets/Screenshot 2021-06-27 at 02.42.14.png>)



Naas is an open-source platform that allows data professionals (business analysts, scientists and engineers) to create data engines combining automation, analytics and AI from the comfort of their Jupyter notebooks.

The data engines unlock the ability to follow live metrics across business domains and generate micro-decisions recommendations for non-tech users.

![](<.gitbook/assets/Screenshot 2022-02-27 at 01.29.24.png>)

The platform is based on 3 elements: templates, drivers, features.

* The templates enable the user to create “ready-to-use” automation and reports in minutes.
* The low-code drivers act as lego blocks to facilitate interconnections between tools (databases, APIs, Machine Learning algorithms...).
* The low-code features (scheduling, asset sharing, notifications...) enable distribution of insights to end-users in multiple channels.

![](<.gitbook/assets/Screenshot 2022-02-27 at 01.54.14 (1).png>)

Naas is forever free to use with 100 credits/month on its hosted version [www.naas.ai](https://www.naas.ai).\
[👉Open your account](https://www.naas.ai/free-forever)&#x20;

## How does it work?

### Start with templates&#x20;

The easiest way to go is simply to find the right template for you.&#x20;

{% content-ref url="templates.md" %}
[templates.md](templates.md)
{% endcontent-ref %}

### Naas services

Naas creates a dynamic production environment for your Notebooks. Each time you run the following formulas in a notebook, it will be sent into the "⚡️ → Production" folder" for execution. &#x20;

To get started, create a folder, open a notebook, and import Naas :

```python
import naas
```

### Schedule your notebook

Send in production this notebook and run it, every day at 9:00&#x20;

```python
naas.scheduler.add(cron="0 9 * * *")
```

{% content-ref url="features/scheduler.md" %}
[scheduler.md](features/scheduler.md)
{% endcontent-ref %}

### Add a dependency

Send in production any file type like `test.csv` as a dependency:

```python
naas.dependency.add("test.csv")
```

{% content-ref url="features/dependency.md" %}
[dependency.md](features/dependency.md)
{% endcontent-ref %}

### Add a secret key

Copy in production any secret key :

```python
naas.secret.add(name="API_NAME", secret="API_KEY")
```

Remove the previous line and get your secret key with :

```python
naas.secret.get(name="MY_API_KEY")
```

This allows you to push your notebook in production without sensitive data getting exposed.&#x20;

{% content-ref url="features/secret.md" %}
[secret.md](features/secret.md)
{% endcontent-ref %}

### Trigger Webhook

Copy in production this notebook and allow to run it by calling the returned URL:

```python
naas.webhook.add()
```

Call the URL with your navigator you will get a message and see the notebook has run.

If you want to download the notebook result instead, add this line:&#x20;

```python
naas.webhook.respond_notebook()
```

{% content-ref url="features/api.md" %}
[api.md](features/api.md)
{% endcontent-ref %}

### Expose assets

Copy in production this asset ( file ) and allow to get it by calling the returned url:

```python
link = naas.assets.add("tesla-chart.html")
```

{% content-ref url="features/asset.md" %}
[asset.md](features/asset.md)
{% endcontent-ref %}

### Send notifications

Send an email notification to anyone, to notify about data changes, alert on notebooks operations, etc...

```python
# Get link var from previous step
email = "elon@musk.com"
subject = "The tesla action is going up"
content = "check in the link the chart data maide from fresh dataset : " + link
naas.notifications.send(email=email, subject=subject, content=content)
```

{% content-ref url="features/notification.md" %}
[notification.md](features/notification.md)
{% endcontent-ref %}

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

## Documentation

Show a button to quickly open this documentation from Jupyter

```python
import naas
naas.doc()
```
