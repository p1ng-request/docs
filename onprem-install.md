---
description: Guide to install Naas on your own
---

# On-prem install

## Before start

Naas is not only a python module, is a set of tools who work perfectly together.

{% hint style="info" %}
You can test on your local computer only Scheduler feature.
{% endhint %}

{% hint style="warning" %}
Full install needs Kubernet and Docker knowledge.
{% endhint %}

## How to install

### Require Env

* `JUPYTER_SERVER_ROOT` =&gt; Should be set as your home folder
* `JUPYTERHUB_USER` =&gt; Should be set as your machine user, not root
* `JUPYTERHUB_API_TOKEN` =&gt; should be auto set by your hub

### **Optional Env** 

* `NAAS_RUNNER_PORT` to change the port of the Naas runner
* `PUBLIC_PROXY_API`for api and assets features your should run the Naas proxy machine and provide his hostname .
* `JUPYTERHUB_URL` the web url of your hub for api and assets features.
* `SCREENSHOT_API` the web url of your screenshot api for plot and other.
* `NOTIFICATIONS_API` for notification feature your should run the Naas notification machine and provide his hostname here
* `NAAS_SENTRY_DSN` to catch error made by your users, configure it.
* `SINGLEUSER_PATH` for Kubernet and your singleusers machine have specific hostname end

```python
!pip install nass
```

Start the server in your Jupyter singleuser machine: 

```bash
!python -m naas.runner &
```

You can now delete both previous cells

## Tools

Below the list of the tools we run to make the perfect notebook experience.

{% hint style="info" %}
Documentation on how to install them, is coming soon.
{% endhint %}

### [Naas](https://hub.docker.com/r/jupyternaas/naas) 

The magic server who take care of your notebooks

### [Proxy](https://hub.docker.com/r/jupyternaas/proxy) 

The proxy who expose the different url for your notebooks

### [Notification](https://hub.docker.com/r/jupyternaas/notifications)

The server who send emails for the users

### [Screenshot](https://hub.docker.com/r/jupyternaas/screenshot)

The server who do html screenshots

### [Jupyter](https://hub.docker.com/r/jupyternaas/lab)

The Jupyter machine who allow user to start they own machine

## 

