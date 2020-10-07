---
description: Make your notebook run at every period
---

# Scheduler

If you don't know cron  : [https://crontab.guru/](https://crontab.guru/)

## Simple

Send in production this notebook and run it, every day at 9:00 :

```python
naas.scheduler.add(recurrence="0 9 * * *")
```

## Other notebook

You can also give a path to the function and that will deploy this one instead of the current one.

```python
naas.scheduler.add(path="path/to/my/super/notebook.ipynb", recurrence="0 9 * * *")
```

## Parameters

`notif_down` : Receive email when notebook run fails.

`notif_up` : Receive email when notebook run well.

```python
params = {"notif_down": "bob@naas.ai", "notif_up": "georges@naas.ai"}

naas.scheduler.add(recurrence="0 9 * * *", params=params)
```

## List current

You don't remember how many Scheduled notebook you have ?

```python
naas.scheduler.currents()
```

Optionally you can get the raw result :

```python
naas.scheduler.currents(raw=True)
```

## Delete

You can remove any scheduler capability like that, it takes optionally a path .

```python
naas.scheduler.delete()
```

## Debug

Need to understand why, something go bad ?

```python
naas.scheduler.add(recurrence="0 9 * * *", debug=True)
```

