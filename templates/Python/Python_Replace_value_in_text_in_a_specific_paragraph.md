<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Replace_value_in_text_in_a_specific_paragraph.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Replace+value+in+text+in+a+specific+paragraph:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #string #replace #text #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to replace a value in a specific paragraph of a text using Python.

<u>References:</u>
- https://www.geeksforgeeks.org/python-string-replace/
- https://www.programiz.com/python-programming/methods/string/replace

## Input

### Import libraries


```python
import re
```

### Setup Variables
- `text`: text containing the paragraph to be modified
- `paragraph`: paragraph to be modified
- `old_value`: value to be replaced
- `new_value`: value to replace the old one


```python
# Setup variables
text = "This is the first paragraph. This is the second paragraph. This is the third paragraph."
paragraph = "This is the second paragraph."
old_value = "second"
new_value = "fourth"
```

## Model

### Replace value in text


```python
# Replace value in text
new_paragraph = re.sub(old_value, new_value, paragraph)
new_text = text.replace(paragraph, new_paragraph)
```

## Output

### Display result


```python
print(new_text)
```
