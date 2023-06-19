<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_currency.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+currency:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #exchange #currency #converter #convert #snippet #operations

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This workbook shows you how to convert any currency into any other currency in real time using `forex_python` library.

**References:**
- [Python Currency converter](https://forex-python.readthedocs.io/en/latest/usage.html)

## Input

### Import libraries


```python
try:
    from forex_python.converter import CurrencyRates
except:
    !pip install forex_python --user
    from forex_python.converter import CurrencyRates
```

### Setup Variables
[Forex Python Available exchange rates](https://github.com/Benjifilly/My_notebooks/wiki/Forex-Python-Available-exchange-rates#real-time-exchange-rates-in-forex-python)
- `amount`: Enter the amount you want to convert
- `from_currency`:  Enter the currency code to convert from
- `to_currency`:  Enter the currency code to convert to


```python
amount = 1  
from_currency = 'USD' 
to_currency = 'EUR'  
```

## Model

### Converting currency


```python
def convert_currency(amount, from_currency, to_currency):
    c = CurrencyRates()
    converted_amount = c.convert(from_currency, to_currency, amount)
    return converted_amount
```

## Output

### Display result


```python
converted_amount = convert_currency(amount, from_currency, to_currency)
print(f"{amount} {from_currency} = {converted_amount} {to_currency}")
```

 
