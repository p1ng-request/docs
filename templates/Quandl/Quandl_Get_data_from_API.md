<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Quandl/Quandl_Get_data_from_API.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #quandl #marketdata #opendata

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

## Input

### Install packages


```python
!pip install quandl
```

### Import libraries


```python
import quandl
import matplotlib.pyplot as plt
```

## Model

### Get the data 


```python
data = quandl.get('EIA/PET_RWTC_D')
```

## Output

### Show dataframe


```python
data
```

### Show the graph


```python
%matplotlib inline
data.plot()
```
