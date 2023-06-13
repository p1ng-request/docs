<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Create_Strong_Random_Password.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Create+Strong+Random+Password:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #password #random #snippet #operations 

**Author:** [Sunny](https://www.linkedin.com/in/sunny-chugh-ab1630177/)

**Description:** The objective of this notebook is to Create Strong random password. 

## Input 

### Import libraries
Import the necessary libraries: random,string


```python
import random
import string
```

### Setup variables


```python
word_length = 18
special_char = "!@#$%&"
```

## Model

### Create strong random passwords


```python
# Generate a list of letters, digits, and some punctuation
components = [string.ascii_letters, string.digits, special_char]

# flatten the components into a list of characters
chars = []
for clist in components:
    for item in clist:
        chars.append(item)

# Store the generated password
password = []
# Choose a random item from 'chars' and add it to 'password'
for i in range(word_length):
    rchar = random.choice(chars)
    password.append(rchar)

# Return the composed password as a string
generated_password = "".join(password)
```

## Output

### Display result


```python
print(f"Password Successfully generated: {generated_password}!")
```
