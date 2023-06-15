<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Find_differences_between_strings.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Find+differences+between+strings:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #strings #differences #compare #find #string

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will compare two strings and find the differences between them. It is useful for users to quickly identify the differences between two strings.

**References:**
- [Python String Comparison](https://www.programiz.com/python-programming/string-comparison)
- [Python String Methods](https://www.programiz.com/python-programming/methods/string)

## Input

### Setup Variables
- `string1`: The first string to compare
- `string2`: The second string to compare


```python
string1 = "hello i'm benjamin"
string2 = "hallo, how are you"
```

## Model

### Find differences between strings

This function will compare two strings and return the differences between them.


```python
def find_string_differences(string1, string2):
    differences = []

    # Find differences between the strings
    for index, (char1, char2) in enumerate(zip(string1, string2)):
        if char1 != char2:
            differences.append(index)

    # Account for differences in length
    if len(string1) > len(string2):
        for index in range(len(string2), len(string1)):
            differences.append(index)

    elif len(string1) < len(string2):
        for index in range(len(string1), len(string2)):
            differences.append(index)

    return differences
differences = find_string_differences(string1, string2)

# Highlight the differences with ANSI escape sequences
highlighted_string1 = ''
highlighted_string2 = ''

for index in range(max(len(string1), len(string2))):
    if index in differences:
        highlighted_string1 += "\033[93m" + (string1[index] if index < len(string1) else '') + "\033[0m"
        highlighted_string2 += "\033[93m" + (string2[index] if index < len(string2) else '') + "\033[0m"
    else:
        highlighted_string1 += string1[index] if index < len(string1) else ' '
        highlighted_string2 += string2[index] if index < len(string2) else ' '
```

## Output

### Display result


```python
# Print the highlighted strings
print(f"String 1: {highlighted_string1}")
print(f"String 2: {highlighted_string2}")
```

 
