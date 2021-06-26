---
description: >-
  How to start using Naas drivers in minutes. Naas drivers are made to
  facilitate scripting with your favorite tools.
---

# Get started

## Welcome to Naas Drivers

If you want to use Naas drivers on your local Jupyter environment, it's free and open-source, just follow the procedure below  :

```python
!pip install naas_drivers
```

{% hint style="warning" %}
Few drivers need a specific env var set, that will be notified 
{% endhint %}

### Why Naas Drivers?

We came from excel with the conviction that Python is awesome.

Python can be used by developers, or in _a low code_ way.

 That what we try to achieve with **naas\_drivers**.

### Simple formulas to interact with powerful tools.

## Version

### Get

the version number in your local machine

```python
import naas_drivers
naas_drivers.version()
```

### Are you at the last version

```python
import naas_drivers

naas_drivers.up_to_date()
```

### Get remote version

the last version number in Github

```python
import naas_drivers
naas_drivers.get_last_version()
```

## Documentation

Show a button to quick open this documentation from Jupyter

```python
import naas_drivers
naas_drivers.doc()
```

## Feature request

show feature request inside Jupyter

```python
import naas
mode = "naas_drivers" # can be naas, naas_drivers, awesome_notebook
naas.feature_request(mode)
```



