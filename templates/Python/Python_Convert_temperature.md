<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_temperature.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+temperature:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #convert #units #snippet #operations #temperature 

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows you how to convert units temperature using Python.

**References:**
- [Python Unit converter example](https://stackoverflow.com/questions/32091117/simple-unit-converter-in-python)

## Input

### Setup Variables
[Unit Available symbols](https://github.com/Benjifilly/My_notebooks/wiki/Unit-symbols#temperature--category-temperature)
- `value`: starting unit value
- `from_unit` : is the unit of the starting value, the one you want to convert
- `to_unit`: this is the unit we want to achieve with this script


```python
value = 100
from_unit = 'C'
to_unit = 'F'
```

## Model

### Unit available


```python
def convert_temperature(value, from_unit, to_unit):
    units = {
        'C': {
            'C': lambda x: x,
            'F': lambda x: x * 9 / 5 + 32,
            'K': lambda x: x + 273.15
        },
        'F': {
            'C': lambda x: (x - 32) * 5 / 9,
            'F': lambda x: x,
            'K': lambda x: (x + 459.67) * 5 / 9
        },
        'K': {
            'C': lambda x: x - 273.15,
            'F': lambda x: x * 9 / 5 - 459.67,
            'K': lambda x: x
        }
    }

    if from_unit not in units or to_unit not in units[from_unit]:
        raise ValueError("Invalid unit.")

    return units[from_unit][to_unit](value)
```

## Output

### Display result


```python
result = convert_temperature(value, from_unit, to_unit)
result
```

 
