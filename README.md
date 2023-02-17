---
description: >-
  These Docs will help you get started with Naas quickly, guide you through
  advanced features, and explain the core concepts that make Naas unique.
cover: >-
  https://images.unsplash.com/photo-1506318137071-a8e063b4bec0?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw1fHxzdGFyc3xlbnwwfHx8fDE2NDM3MDc0ODE&ixlib=rb-1.2.1&q=85
coverY: 0
---

# Get Started

{% hint style="warning" %}
This documentation is in `beta`. It may change frequently. To propose changes or enhancements, please create a [GitHub Issue.](https://github.com/jupyter-naas/docs)&#x20;
{% endhint %}

## Welcome to Naas!

Notebooks as a service (Naas) is an open source platform that allows anyone touching data (analysts, scientists and engineers) to create powerful data solutions combining automation, analytics and AI from the comfort of their Jupyter notebooks.

Naas is an alternative to Google Colab, with superpowers.

The platform upgrades notebooks with 3 low-code layers to get things done faster: features, drivers, and templates.

* ****[**Templates**](templates.md) enable the user to create automated data jobs and reports in minutes.
* ****[**Drivers**](drivers/) act as connectors to push and/or pull data from databases, APIs, Machine Learning algorithms, and more.
* ****[**Features**](features/) transform Jupyter in a production-ready environment with scheduling, asset sharing, and notifications.

## Naas Cloud

Naas cloud is the fastest and easiest way to get you started!

Try all of Naas's features for free using [Naas cloud](https://app.naas.ai/hub/login) a stable environment, without having to install anything.

## How to use Naas Cloud?

### Start with templates&#x20;

The easiest way to go is simply to find the right template for you.&#x20;

{% content-ref url="templates.md" %}
[templates.md](templates.md)
{% endcontent-ref %}

### Naas services

Naas creates a dynamic production environment for your Notebooks. Each time you run the following formulas in a notebook, it will be sent into the "\_\_production\_\_" folder on your Naas server for execution. &#x20;

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
link = naas.asset.add("tesla-chart.html")
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
naas.notification.send(email=email, subject=subject, content=content)
```

{% content-ref url="features/notification.md" %}
[notification.md](features/notification.md)
{% endcontent-ref %}

### Help

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

### Documentation

Show a button to quickly open this documentation from Jupyter

```python
import naas
naas.doc()
```

## Contributing

We value all kinds of contributions - not just code. We are particularly motivated to support new contributors and people who are looking to learn and develop their skills.

Please read our [Contributing guidelines](contributing-to-naas/contributing.md) on how to get started.

## Community Support

You can reach out to us through the following channels:

* [Slack](https://join.slack.com/t/naas-club/shared\_invite/zt-1970s5rie-dXXkigAdEJYc\~LPdQIEaLA) (Live Discussions)
* [GitHub Issues](https://github.com/jupyter-naas/naas/issues/new) (Report Bugs)
* [Twitter](https://twitter.com/JupyterNaas) (Latest News)
* [YouTube](https://www.youtube.com/c/naas-ai) (Video Tutorials)
* [Community calls ](https://calendar.google.com/calendar/u/0/embed?src=c\_aultg6lanla9l39k8f5fm7d264@group.calendar.google.com\&ctz=Europe/Paris)(Video call discussions with the naas team & other contributors.)

