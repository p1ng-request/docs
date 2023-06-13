<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Validate_email_and_phone_numbers.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Validate+email+and+phone+numbers:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #twilio #project #call #mobile #snippet

**Author:** [Sriniketh Jayasendil](https://twitter.com/srini047/)

**Description:** This notebook validates a given email address and phone number using `re` and `phonenumbers` modules.

**References:**
- [re — Regular expression operations](https://docs.python.org/3/library/re.html)
- [PyPI - phonenumbers](https://pypi.org/project/phonenumbers/)

## Input

### Import librairies


```python
import re
try:
    import phonenumbers
except ModuleNotFoundError:
    !pip install phonenumbers
    import phonenumbers
```

### Setup Variables
You can build and test regular expression patterns using this [regex101.com](https://regex101.com/)
- `email_regex`: Pattern to match Email Address


```python
email_regex = "^[a-z0-9]+[\._]?[a-z0-9]+[@]\w+[.]\w{2,3}$"  # Pattern to match Email Address
```

## Model

### Check email function


```python
def check_email(email):
    if re.fullmatch(email_regex, email):
        print("Valid Email✅")
    else:
        print("Invalid Email❌")
```

### Check phone number function


```python
def check_phone_number(phone_number):
    phone_number = phonenumbers.parse(phone_number)
    possible = phonenumbers.is_valid_number(phone_number)
    if possible:
        if phonenumbers.is_possible_number(phone_number):
            print("Valid Phone Number✅")
    else:
        print("Invalid Phone Number❌")
```

## Output

### Check email and phone number


```python
input_email = input("Enter the Email-ID: ")
check_email(input_email)

input_phone_number = input("Enter the Phone Number (please start with your country ID like +33 for France): ")
check_phone_number(input_phone_number)
```


```python

```
