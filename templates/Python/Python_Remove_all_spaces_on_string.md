<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Remove_all_spaces_on_string.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Remove+all+spaces+on+string:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #remove #string #space 

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows how to remove all spaces from a string using two different methods 

**References:**
- [Python tutorial: deleting spaces](https://www.geeksforgeeks.org/python-remove-spaces-from-a-string/)


## Input

### Setup Variables
- `string`: character string space you want to remove


```python
string = "Hello, world! This is a string with spaces."
```

## Model

### Method 1 : Delete all space using replace
In this example, the `replace()` method is called on the `string` variable. It takes two arguments: the substring to be replaced (" ") and the new substring to replace it with ("").

Note that the `replace()`method returns a new string with the replacements made, while the original string remains unchanged.


```python
string_without_spaces1 = string.replace(" ", "")
string_without_spaces1
```

### Method 2: Using join and split method 

- `string.split()` : The`split()`method is called on the `string`variable without any arguments. It divides the string into a list of substrings, using space characters (spaces, tabs or line breaks) as delimiters.
- `"".join` : The `join()` method is called on an empty string `""` and takes the result of `string.split()` as argument. It concatenates the substrings of the list together, using the empty string as separator.




```python
string_without_spaces2 = "".join(string.split())
string_without_spaces2
```

## Output

### Display result 1


```python
print("String without spaces:", string_without_spaces1)
```

 

### Display result 2


```python
print("String without spaces:", string_without_spaces2)
```
