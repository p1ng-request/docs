<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Set_timezone.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #naas #timezone

## Input

### Import needed library


```python
import naas
```

### Get your current timezone


```python
naas.get_remote_timezone()
```

## Model

### Select your timezone
[Wikipedia timezones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)


```python
new_timezone = "Europe/Paris"
```

## Output

### Set your new timezone


```python
naas.set_remote_timezone(new_timezone)
```
