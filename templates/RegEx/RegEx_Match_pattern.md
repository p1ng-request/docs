<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/RegEx/RegEx_Match_pattern.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=RegEx+-+Match+pattern:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #regex #python #snippet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook demonstrates how to match a pattern in a string using `re.search()` and `re.match()`. The main difference between `re.search()` and `re.match()` lies in how they apply pattern matching to the input string. `re.search()` scans the entire input string and returns the first occurrence of a pattern match, regardless of its position within the string. On the other hand, `re.match()` only checks for a pattern match at the beginning of the string.

To start, we recommand you to test your regular expression using this website: https://regex101.com/

**References:** 
- [re — Regular expression operations](https://docs.python.org/3/library/re.html)

## Input

### Import libraries


```python
import re
```

### Setup Variables
- `pattern`: the email address to be checked
- `input_string`: the email address to be checked


```python
pattern = "\d+"
input_string = "Temperature: 0°C"
```

## Model

### Match pattern using re.search()


```python
search_result = re.search(pattern, input_string)
search_result
```

### Match pattern using re.match()


```python
match_result = re.match(pattern, input_string)
match_result
```

## Output

### Display result
When we use re.match() with the same pattern, it fails to find a match because the pattern is only checked at the beginning of the string. Since "0" is not at the beginning, re.match() returns no match.


```python
if search_result:
    print("Search Result:", search_result.group())
else:
    print("No match found with re.search()")
    
if match_result:
    print("Match Result:", match_result.group())
else:
    print("No match found with re.match()")
```

 


```python

```
