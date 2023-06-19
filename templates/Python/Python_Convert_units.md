<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_units.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+units:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #convert #units #snippet #operations #length #temperature #weight #time #volume #speed

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows you how to convert units (length, temperature, weight, time, volume, speed) using Python.

**References:**
- [Python Unit converter example](https://stackoverflow.com/questions/32091117/simple-unit-converter-in-python)

## Input

### Setup Variables
[Unit Available symbols](https://github.com/Benjifilly/My_notebooks/wiki/Unit-symbols)
- `value`: starting unit value
- `from_unit` : is the unit of the starting value, the one you want to convert
- `to_unit`: this is the unit we want to achieve with this script
- `category`: the category to which the units belong


```python
value = 20
from_unit = 'C'
to_unit = 'F'
category = 'temperature'
```

## Model

### Unit available


```python
def convert_length(value, from_unit, to_unit):
    units = {
        'mm': 0.001,
        'cm': 0.01,
        'm': 1.0,
        'km': 1000.0,
        'in': 0.0254,
        'ft': 0.3048,
        'yd': 0.9144,
        'mi': 1609.34,
        'nm': 1e-9,
        'μm': 1e-6,
        'mil': 0.0254 / 1000,
        'fm': 1e-15
        # Add other length units here
    }

    if from_unit not in units or to_unit not in units:
        raise ValueError("Invalid unit.")

    return value * units[from_unit] / units[to_unit]


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


def convert_weight(value, from_unit, to_unit):
    units = {
        'mg': 0.001,
        'g': 1.0,
        'kg': 1000.0,
        'lb': 453.592,
        'oz': 28.3495,
        't': 1000000.0,
        'st': 6350.29318,
        'carat': 0.2,
        'grain': 0.06479891
        # Add other weight units here
    }

    if from_unit not in units or to_unit not in units:
        raise ValueError("Invalid unit.")

    return value * units[from_unit] / units[to_unit]


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


def convert_volume(value, from_unit, to_unit):
    units = {
        'mL': 0.001,
        'L': 1.0,
        'gal': 3.78541,
        'qt': 0.946353,
        'pt': 0.473176,
        'fl oz': 0.0295735,
        'm3': 1000.0
        # Add other volume units here
    }

    if from_unit not in units or to_unit not in units:
        raise ValueError("Invalid unit.")

    return value * units[from_unit] / units[to_unit]


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

### Converting


```python
def convert_units(value, from_unit, to_unit, category):
    if from_unit == to_unit:
        return value

    if category == 'length':
        return convert_length(value, from_unit, to_unit)

    elif category == 'temperature':
        return convert_temperature(value, from_unit, to_unit)

    elif category == 'weight':
        return convert_weight(value, from_unit, to_unit)

    elif category == 'time':
        return convert_time(value, from_unit, to_unit)

    elif category == 'volume':
        return convert_volume(value, from_unit, to_unit)

    elif category == 'speed':
        return convert_speed(value, from_unit, to_unit)

    else:
        raise ValueError("Unsupported unit category.")
```

## Output

### Display result


```python
result = convert_units(value, from_unit, to_unit, category)
print("{} {} to {} = {}".format(value, from_unit, to_unit, result))
```

 
