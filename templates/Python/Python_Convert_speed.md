<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_speed.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+speed:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #convert #units #snippet #operations #speed

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows you how to convert speed using Python.

**References:**
- [Python Unit converter example](https://stackoverflow.com/questions/32091117/simple-unit-converter-in-python)

## Input

### Setup Variables
[Unit Available symbols](https://github.com/Benjifilly/My_notebooks/wiki/Unit-symbols#speed--category-speed)
- `value`: starting unit value
- `from_unit` : is the unit of the starting value, the one you want to convert
- `to_unit`: this is the unit we want to achieve with this script


```python
value = 50
from_unit = 'km/h'
to_unit = 'm/s'
```

## Model

### Unit available


```python
def convert_speed(value, from_unit, to_unit):
    units = {
        'm/s': 1.0,
        'km/h': 1 / 3.6,
        'mph': 0.44704,
        'knot': 0.514444
        # Add other speed units here
    }

    if from_unit not in units or to_unit not in units:
        raise ValueError("Invalid unit.")

    return value * units[from_unit] / units[to_unit]
```

## Output

### Display result


```python
result = convert_speed(value, from_unit, to_unit)
result
```

 
