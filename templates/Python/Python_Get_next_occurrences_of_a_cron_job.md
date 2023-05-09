<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Get_next_occurrences_of_a_cron_job.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Get+next+occurrences+of+a+cron+job:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #cron #croniter #job #occurrences #scheduling

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get the next x occurrences of your cron job using croniter. It is usefull for organizations to schedule tasks and jobs.

**References:**
- [croniter](https://pypi.org/project/croniter/#usage)
- [cron](https://en.wikipedia.org/wiki/Cron)

## Input

### Import libraries


```python
try:
    import croniter
except:
    !pip install croniter --user
    import croniter
import pytz
from datetime import datetime
```

### Setup Variables
- `cron_expression`: cron expression to be used
- `occurrences`: number of occurrences to be returned
- `timezone`: timezone identifier


```python
cron_expression = "*/15 * * * *"
occurrences = 5
timezone = 'Europe/Paris'
```

## Model

### Set the timezone


```python
# Set the timezone
tz = pytz.timezone(timezone)
```

### Create a cron iterator


```python
# Create a cron iterator with the timezone
cron = croniter.croniter(cron_expression, datetime.now(tz), tz)
```

## Output

### Get the next x occurrences of the cron job and convert them to text


```python
for i in range(occurrences):
    next_occurrence = cron.get_next(datetime)
    print(next_occurrence.strftime('%A, %B %d, %Y at %I:%M %p'))
```

 
