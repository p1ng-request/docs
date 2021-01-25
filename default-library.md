---
description: List of lib installed in your naas machine (cloud only)
---

# 💃 Default Library

{% hint style="info" %}
All library listed below are essential to naas, please don't update them !
{% endhint %}

## Python level

```text
    "nbconvert>=6,<7",
    "ipywidgets>=7,<8",
    "sentry_sdk>=0,<1",
    "papermill>=2,<3",
    "pretty-cron>=1,<2",
    "APScheduler>=3,<4",
    "pycron>=3,<4",
    "html5lib>=1,<2",
    "Pillow>=8,<9",
    "markdown2>=2,<3",
    "pandas>=1,<2",
    "daemonize>=2,<3",
    "escapism>=1,<2",
    "notebook>=6,<7",
    "ipython>=7,<8",
    "ipykernel>=5,<6",
    "requests>=2,<3",
    "sentry-sdk>=0,<1",
    "sanic>=20,<21",
    "sanic-openapi>=0,<1",
    "argparse>=1,<2",
    "nbconvert>=6,<7",
    "nbclient>=0,<1",
    "beautifulsoup4>=4,<5",
    "jupyterhub==1.3.0",
    "jupyterlab==2.2.92.2.9",
    "jupyter_client==6.1.7",
    "jupyterlab-git==0.23.3",
    "nbdime==2.1.0",
    "nbformat",
    "nbconvert",
    "nbresuse",
    "ipyparallel",
    "ipywidgets",
    "ipympl==0.5.8",
    "jupyter-server-proxy",
    "jupyter-launcher-shortcuts",
    "matplotlib==3.3.1"
```

## Machine Level

```text
redir 
tzdata
tesseract-ocr
libtesseract-dev
libcairo2-dev
```

## Base image

Below you can find all packages installer by the jupyter team, we use this docker image as base for our own build. 

{% embed url="https://github.com/jupyter/docker-stacks/blob/master/minimal-notebook/Dockerfile" %}



