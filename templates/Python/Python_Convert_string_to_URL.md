<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_string_to_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+string+to+URL:+Error+short+description">Bug report</a>

**Tags:** #python #urllib #string #url #convert #library

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to convert a string to a URL using urllib.

**References:**
- [urllib documentation](https://docs.python.org/3/library/urllib.parse.html)
- [Python 3 Tutorial - String to URL](https://www.tutorialspoint.com/python3/python_strings.htm)

## Input

### Import libraries


```python
import urllib.parse
```

### Setup Variables
- `string`: string to be converted to URL


```python
string = "This is a string"
```

## Model

### Convert string to URL
The `quote()` function replaces special characters in the string with their percent-encoded equivalent, which is necessary for URLs. The resulting URL can be used in your Python code or in a web browser. <br>
Note that if you need to convert the URL back to a string, you can use the unquote() 


```python
url = urllib.parse.quote(string)
```

## Output

### Display result


```python
print(url)
```

 
