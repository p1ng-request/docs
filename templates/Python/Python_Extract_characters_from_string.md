<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Extract_characters_from_string.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Extract+characters+from+string:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #extract #string #character

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will show how to extract characters from a string.

**References:**
- [Python Extraction method](https://note.nkmk.me/en/python-str-extract/#:~:text=You%20can%20extract%20a%20substring%20in%20the%20range%20start%20%3C%3D%20x,the%20end%20of%20the%20string.&text=You%20can%20also%20use%20negative%20values.&text=If%20start%20%3E%20end%20%2C%20no%20error,empty%20string%20''%20is%20extracted.)

## Input

### Setup Variables
- `string`: character string to be extracted
- `start_string`: It represents the starting index position of the substring in the variable `string`.
- `end_string`: It represents the ending index position (exclusive) of the substring in the variable `string`.
- `step`: It determines the step or stride size used to select characters from the `string`. In this case, every second character is selected due to a step value of 2.


```python
string = "Hello, World!"
start_string = 7
end_string = 12
step = 2
```

## Model

### Extract characters using index


```python
substring = string[start_string:end_string]
substring
```

### Extract characters using steps


```python
steps = string[::step]
steps
```

## Output

### Display result 1


```python
print(string)
print(f"Characters extracted from index '{start_string}' to index '{end_string}':", substring)
```

### Display result 2


```python
print(string)
print(f"Characters extracted every every '{step}' step started at 0:", steps)
```

 
