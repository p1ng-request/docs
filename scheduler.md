---
description: Get more options in scheduler system
---

# Scheduler

## Basic

Send in production this notebook and run it, every day at 9:00 :

```python
naas.scheduler.add(recurrence="0 9 * * *")
```

## Other file

You can also give a path to the function and that will deploy this one instead of the current one.

```python
naas.scheduler.add(path="path/to/my/super/notebook.ipynb", recurrence="0 9 * * *")
```



