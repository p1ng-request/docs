<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_Datetime_with_Timezone_to_ISO_8601_date_string.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+Datetime+with+Timezone+to+ISO+8601+date+string:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #datetime #timezone #iso8601 #string #conversion

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to convert a datetime with timezone to an ISO 8601 date string.

<u>References:</u>
- [Python datetime](https://docs.python.org/3/library/datetime.html)
- [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)

## Input

### Import libraries


```python
from datetime import datetime
import pytz
```

### Setup Variables
- `date_time`: datetime with timezone


```python
date_time = datetime(2020, 8, 1, 12, 0, 0, tzinfo=pytz.timezone("Europe/Paris"))
print(date_time)
```

## Model

### Convert datetime with timezone to ISO 8601 date string


```python
iso_date_string = date_time.isoformat()
```

## Output

### Display result


```python
print(iso_date_string)
```

 
