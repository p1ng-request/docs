<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_time.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+time:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #convert #units #snippet #operations #time 

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows you how to convert time using Python.

**References:**
- [Python Unit converter example](https://stackoverflow.com/questions/32091117/simple-unit-converter-in-python)

## Input

### Setup Variables
[Unit Available symbols](https://github.com/Benjifilly/My_notebooks/wiki/Unit-symbols#time--category-time)
- `value`: starting unit value
- `from_unit` : is the unit of the starting value, the one you want to convert
- `to_unit`: this is the unit we want to achieve with this script


```python
value = 3600
from_unit = 's'
to_unit = 'h'
```

## Model

### Unit available


```python
def convert_time(value, from_unit, to_unit):
    units = {
        's': 1.0,
        'min': 60.0,
        'h': 3600.0,
        'day': 86400.0,
        'week': 604800.0,
        'month': 2628000.0,
        'year': 31536000.0
        # Add other time units here
    }

    if from_unit not in units or to_unit not in units:
        raise ValueError("Invalid unit.")

    return value * units[from_unit] / units[to_unit]
```

## Output

### Display result


```python
result = convert_time(value, from_unit, to_unit)
result
```

 
