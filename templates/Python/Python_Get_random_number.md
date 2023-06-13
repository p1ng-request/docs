<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Get_random_number.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Get+random+number:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #number #generation #random #snippet #operation

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook demonstrates how to get random numbers.

**References:**
- [Python Random](https://docs.python.org/3/library/random.html)

## Input

### Import libraries


```python
import random
```

### Setup Variables
- `number_start`: integer to be used as first number in random.randrange and random.randint 
- `number_end`: integer to be used as the last number in random.randrange and random.randint 
- `step`: step to be used to get random number using random.randrange, default = 1


```python
number_start = 0
number_end = 500
step = 100
```

## Model

### Get random decimal


```python
random_decimal_number = random.random()
```

### Get random integer


```python
random_integer_number = random.randint(number_start, number_end)
```

### Get random integer from range


```python
random_number = random.randrange(number_start, number_end, step)
```

## Output

### Display result


```python
print("The random decimal number generated is", random_decimal_number)
print("The random integrer number generated is", random_integer_number)
print("The random number generated is", random_number, "with a step of", step)
```

 
