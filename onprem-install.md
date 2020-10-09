---
description: Install Naas on a Kubernetes environment.
---

# ☁️ Deploy on Kubernetes

## Before your start

Naas is not only a python module, it's a set of tools that work perfectly together.

## Naas Tools

Below the set of tools we run to build the perfect notebook experience.

{% hint style="info" %}
Documentation on how to install them, is coming soon.
{% endhint %}

### [Naas](https://hub.docker.com/r/jupyternaas/naas) 

The magic server who takes care of your notebooks.

### [Proxy](https://hub.docker.com/r/jupyternaas/proxy) 

The proxy who expose the different URL for your notebooks.

### [Notification](https://hub.docker.com/r/jupyternaas/notifications)

The server sending rich email notifications to yourself \(or your audience\).

### [Screenshot](https://hub.docker.com/r/jupyternaas/screenshot)

The server who do HTML screenshots on any website.

### [Jupyter Lab](https://hub.docker.com/r/jupyternaas/lab)

The Jupyter machine who allow users to start their own machine on the cloud.

## Set your local environment

{% hint style="info" %}
You should set them in your Jupyter config file.
{% endhint %}

### **Advanced env :**

* `NAAS_RUNNER_PORT` to change the port of the Naas runner
* `PUBLIC_PROXY_API`for API and assets features you should run the Naas proxy machine and provide a hostname.
* `JUPYTERHUB_URL` the web URL of your hub for API and asset features.
* `SCREENSHOT_API` the web URL of your screenshot API for plot and other.
* `NOTIFICATIONS_API` for the notifications feature, you should run the Naas notification machine and provide a hostname.
* `NAAS_SENTRY_DSN` to catch errors made by your users, configure it.
* `SINGLEUSER_PATH` for Kubernetes and your single-user machine have specific hostname end

