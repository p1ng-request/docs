<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_URL_to_string.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+URL+to+string:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #urllib #string #url #convert #library

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to convert a URL to a string using urllib.

**References:**
- [urllib Documentation](https://docs.python.org/3/library/urllib.html)
- [Python Tutorial - Convert URL to string](https://www.pythonforbeginners.com/urllib/how-to-use-urllib-in-python)

## Input

### Import libraries


```python
import urllib.parse
```

### Setup Variables
- `url`: URL to be converted to string


```python
url = "https://www.pythonforbeginners.com/urllib/how-to-use-urllib-in-python"
```

## Model

### Convert URL to string
The unquote() function in urllib.parse converts percent-encoded characters in the URL back to their original form. In this example, the URL is already in string form, so unquote() simply returns the same string.<br>
If the URL had any percent-encoded characters, they would be decoded by unquote().


```python
string = urllib.parse.unquote(url)
```

## Output

### Display result


```python
print(string)
```

 
