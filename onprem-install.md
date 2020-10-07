---
description: Guide to install Naas on your own
---

# On-prem install

## Before start

Naas is not only a python module, is a lot of tools who work perfectly together, our install work only with Kubernet for now .

## Tools

Below the list of the tools we run to make the perfect notebook experience.

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

#### ENV 

* `NAAS_RUNNER_PORT` to change the port of the Naas runner
* `PUBLIC_PROXY_API` if you want the api and assets features your should run the Naas proxy machine and provide his hostname .
* `JUPYTERHUB_URL` the web url of your hub for api and assets features.
* `SCREENSHOT_API` the web url of your screenshot api for plot and other.
* `NOTIFICATIONS_API` if you want the notification feature your should run the Naas notification machine and provide his hostname here
* `NAAS_SENTRY_DSN` If you need to catch error made by your users, configure it.
* `SINGLEUSER_PATH` if you deploy on Kubernet and your singleusers have specific hostname end

