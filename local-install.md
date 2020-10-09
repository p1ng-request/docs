---
description: Install Naas in your local Jupyter environment.
---

# 🖥️ Use on your computer

## Is your local env ready?

Open a new notebook and then check if the require env is set :

```python
import os
print('Yes' if (os.getenv('NB_USER') and os.getenv('JUPYTERHUB_USER') and os.getenv('JUPYTERHUB_API_TOKEN')) else 'No')
print(os.getenv('NB_USER'), os.getenv('JUPYTERHUB_USER'), os.getenv('JUPYTERHUB_API_TOKEN'))
```

#### Require Env

* `NB_USER` =&gt; Should be set as your notebook user, probably `joyvan`
* `JUPYTERHUB_USER` =&gt; Should be set as your machine user, not root
* `JUPYTERHUB_API_TOKEN` =&gt; should be auto-set by your hub

## Install

Naas is a python module, install it with:

```python
!pip install nass
```

{% hint style="warning" %}
You can test on your local computer only the Scheduler feature.
{% endhint %}

{% hint style="danger" %}
Full install needs Kubernetes and Docker. Let's talk.
{% endhint %}

{% page-ref page="onprem-install.md" %}

## Start

Start the server in your Jupyter singleuser machine: 

```bash
!python -m naas.runner &
```

{% hint style="info" %}
You can now delete previous cells
{% endhint %}

It will run until you stop your Jupyter server, go back to:

{% page-ref page="./" %}



