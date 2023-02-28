<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Create_Email_Combination_with_Firstname_Lastname_Domain_address.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Create+Email+Combination+with+Firstname+Lastname+Domain+address:+Error+short+description">Bug report</a>

**Tags:** #python #email #combination #firstname #lastname #domain #sales #prospect

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will create a list of emails combination with firstname, lastname and domain address. This notebook can be used to find and test an email address for a prospect.

**References:**
- [Python String Formatting Best Practices](https://realpython.com/python-string-formatting/)

## Input

### Import libraries


```python

```

### Setup Variables
- `firstname`: firstname of the person
- `lastname`: lastname of the person
- `domain`: domain address


```python
firstname = "John"
lastname = "Doe"
domain = "example.com"
```

## Model

### Create Emails


```python
def create_emails(firstname, lastname, domain):
    # Init
    emails = []
    
    # Cleaning
    firstname = firstname.lower()
    lastname = lastname.lower()
    domain = domain.lower()
    
    # Create emails
    emails.append(f"{firstname}.{lastname}@{domain}")
    emails.append(f"{firstname}{lastname}@{domain}")
    
    emails.append(f"{lastname}.{firstname}@{domain}")
    emails.append(f"{lastname}{firstname}@{domain}")
    
    emails.append(f"{firstname[:1]}.{lastname}@{domain}")
    emails.append(f"{firstname[:1]}{lastname}@{domain}")
    
    emails.append(f"{firstname}.{lastname[:1]}@{domain}")
    emails.append(f"{firstname}{lastname[:1]}@{domain}")
    return emails
```

## Output

### Display result


```python
emails = create_emails(firstname, lastname, domain)
print(emails)
```

 
