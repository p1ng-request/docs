<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Boursorama/Boursorama_Get_EURIBOR_3_MOIS.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Boursorama+-+Get+EURIBOR+3+MOIS:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #boursorama #euribor #pandas #read_html #finance #data

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to get EURIBOR 3 MOIS using pandas.read_html().

**References:**
- [Boursorama](https://www.boursorama.com/bourse/indices/euribor-3-mois-0D0003M0GQ)
- [Pandas.read_html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_html.html)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `url`: URL of the Boursorama page to get EURIBOR 3 MOIS


```python
url = "https://www.boursorama.com/bourse/taux/cours/2xERB3MOIS/"
```

## Model

### Get EURIBOR 3 MOIS
Using `pandas.read_html()` to get the EURIBOR 3 MOIS from the Boursorama page.


```python
tables = pd.read_html(url)
```

## Output

### Current data


```python
tables[0]
```

### Historical data


```python
tables[1]
```

 
