<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Split_string.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Split+string:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #file #string #url #split #snippet #operations

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook shows you how to split a string object. The `split()` function in Python is useful for dividing a string into smaller parts based on a specified delimiter. It enables efficient string parsing, data cleaning, user input processing, and tokenization in natural language processing tasks.

**References:**
- [Python Tutorial String split](https://www.geeksforgeeks.org/python-string-split/)

## Input

### Setup Variables
- `string`: string to divide
- `separator` : This is a delimiter. The string splits at this specified separator. If is not provided then any white space is a separator.
- `maxsplit`: It is a number, which tells us to split the string into maximum of provided number of times. If it is not provided then the default is -1 that means there is no limit.


```python
string = "/home/user/Documents/example.txt" #the file path or URL you want to separate
separator = "/"
maxsplit = -1
```

## Model

### Split file path or URL


```python
result = string.split(separator, maxsplit)
```

## Output

### Display result


```python
print(result)
```

 
