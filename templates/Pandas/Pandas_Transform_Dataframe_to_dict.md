<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Transform_Dataframe_to_dict.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Transform+Dataframe+to+dict:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #dict #snippet #yahoofinance #naas_drivers #operations #jupyternotebooks

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides an example of how to use the Pandas library to convert a dataframe into a dictionary.

**References:**
- [Pandas DataFrame to_dict](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_dict.html)

## Input

### Import libraries


```python
from naas_drivers import yahoofinance
```

### Setup Variables
- `ticker`: This variable is used to represent the stock ticker symbol
- `date_from`: This variable is used to represent a date offset, where a negative value indicates a date in the past. For example, if today is May 9th, 2023, then date_from represents a date 100 days before May 9th, 2023.
- `date_to`: This variable is used to represent the current date or today's date. The string value "today" can be used to obtain the current date or you need to use to following format "%Y-%m-%d".
- `orient` : Determines the type of the values of the dictionary ('dict', 'list', 'series', 'split', 'tight', 'records', 'index')


```python
# Inputs
ticker = "TSLA"
date_from = -100
date_to = "today"

# Outputs
orient = "records"
```

## Model

### Get dataframe from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker, date_from=date_from, date_to=date_to)
df_yahoo
```

## Output

### Transform Dataframe


```python
dict_yahoo = df_yahoo.to_dict(orient=orient)
dict_yahoo
```
