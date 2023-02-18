# Upgrading Naas

In naas cloud, we push updates every day with our CI /CD, we value stability for you over everything so only new users get the last news.

If you want the last news you can reboot your machine or wait the monthly update, every second day of the month.

## Version

### Get

the version number in your local machine

```python
import naas
naas.version()
```

### Are you at the last version?

```python
import naas

naas.up_to_date()
```

### Get remote version

the last version number in Github

```python
import naas
naas.get_last_version()
```

## To get the latest version&#x20;

### In Naas Cloud

```python
import naas
naas.update()
```

### In your local machine

```python
!pip install --upgrade naas
```

Alternatively, for the more tech people you can see our changelog here :

{% embed url="https://github.com/jupyter-naas/naas/blob/main/CHANGELOG.md" %}

