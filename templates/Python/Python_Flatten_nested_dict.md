<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Flatten_nested_dict.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Flatten+nested+dict:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #dict #flatten #nested #data #structure

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to flatten a nested dict in Python.

**References:**
- [Python - Flatten a nested dictionary, preserving keys](https://stackoverflow.com/questions/6027558/flatten-nested-dictionaries-compressing-keys)
- [Python - How to flatten a shallow list](https://stackoverflow.com/questions/952914/how-to-make-a-flat-list-out-of-list-of-lists)

## Input

### Import libraries


```python

```

### Setup Variables


```python
# Setup a nested dict
nested_dict = {"key1": 1, "key2": {"key3": 1, "key4": {"key5": 4}}}
```

## Model

### Flatten nested dict


```python
# Flatten the nested dict
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)


flatten_dict = flatten_dict(nested_dict)
```

## Output

### Display result


```python
# Display the flatten dict
flatten_dict
```

 
