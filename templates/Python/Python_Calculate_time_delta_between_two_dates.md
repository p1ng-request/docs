<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Calculate_time_delta_between_two_dates.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Calculate+time+delta+between+two+dates:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #datetime #timedelta #calculate #date #time 

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook calculates the time delta between two dates.

**References:**
- [Python datetime](https://docs.python.org/3/library/datetime.html)
- [Python timedelta](https://docs.python.org/3/library/datetime.html#timedelta-objects)

## Input

### Import libraries


```python
from datetime import datetime
```

### Setup Variables
- `start_date`: First date
- `end_date`: Second date


```python
start_date = datetime(2022, 1, 15)
end_date = datetime(2023, 5, 22)
```

## Model

### Calculate time delta

Calculate the time delta between two dates using the `timedelta` function from the `datetime` library.


```python
delta = end_date - start_date
```

## Output

### Display result


```python
print(delta)
```

 
