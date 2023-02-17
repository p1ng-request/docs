<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Check_email_validity.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Check+email+validity:+Error+short+description">Bug report</a>

**Tags:** #python #email #validity #check #regex #string

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will demonstrate how to check the validity of an email address using Python.

<u>References:</u>
- [Python Regular Expressions](https://docs.python.org/3/library/re.html)
- [Python String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

## Input

### Import libraries


```python
import re
```

### Setup Variables
- `email`: the email address to be checked


```python
email = "florent.ravenel@gmail.com"
```

## Model

### Check email validity

This function will check the validity of an email address using a regular expression.


```python
def check_email_validity(email):
    regex = "^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$"
    if re.search(regex, email):
        return True
    else:
        return False
```

## Output

### Display result


```python
print(check_email_validity(email))
```

 
