<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Manage_exception_with_try_except.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Manage+code+error+with+try+except:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #error #try #exception #snippet

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will demonstrate how to manage code error using try except. 
The `try` block lets you test a block of code for errors.
The `except` block lets you handle the error. You can specify the type of exception to manage error.
The `else` block lets you execute code when there is no error.
The `finally` block lets you execute code, regardless of the result of the try- and except blocks.

**References:**
- [Python Try Except](https://www.w3schools.com/python/python_try_except.asp)
- [Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)

## Input

### Setup Variables
- `numérator`: is the numerator of the division
- `denominator`: is the denominator of the division


```python
numerator = 10
denominator = 0
```

## Model

### Try Except example

In this case, We divide `numerator` by the `denominator` and we cannot divide the numerator by 0, so we get an error but we can handle it with `except`. <br>
The `else` block lets you execute code when there is no error and the `finally` block lets you execute code, regardless of the result of the try- and except blocks.




```python
try:
    result = numerator / denominator
except Exception as e:
    result = f"Exception error: {e}"
    print(result)
else:
    print("Nothing went wrong")
finally:
    print("The bloc `finally` is executed anyway")
```

## Output

### Display result


```python
print("Result:", result)
```

 

 
