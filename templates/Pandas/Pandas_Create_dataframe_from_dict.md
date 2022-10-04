<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Create_dataframe_from_dict.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #pandas #dict #snippet #dataframe #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

Here below you will find how to create a pandas DataFrame from a simple dict

## Input

### Import libraries


```python
import pandas as pd
```

### Setup your dict


```python
my_dict = {"LABEL": 1995, "VALUE": 219}
```

## Model

### Create dataframe


```python
df = pd.DataFrame([my_dict])
df
```

## Output

### Display result


```python
df
```
