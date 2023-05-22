<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_relative_time_delta_to_months.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+relative+time+delta+to+months:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #datetime #relativedelta #calculate #date #time #dateutil

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook is designed to convert the relative time delta between two dates into months. By utilizing the `relativedelta` function, the conversion becomes more accurate compared to using `timedelta`, as `relativedelta` considers the varying number of days in each month.

**References:**
- [Python datetime](https://docs.python.org/3/library/datetime.html)
- [Python dateutil](https://pypi.org/project/python-dateutil/)

## Input

### Import libraries


```python
from datetime import datetime
from dateutil.relativedelta import relativedelta
```

### Setup Variables
- `start_date`: First date
- `end_date`: Second date


```python
start_date = datetime(2022, 1, 15)
end_date = datetime(2023, 5, 22)
```

## Model

### Calculate delta and convert to months

Calculate the time delta between two dates using the `relativedelta` function from the `dateutil` library.


```python
delta = relativedelta(end_date, start_date)
months = round(delta.days / 30 + delta.months + 12 * delta.years, 1)
```

## Output

### Display result


```python
print(f"The time delta is {months} months.")
```

 
