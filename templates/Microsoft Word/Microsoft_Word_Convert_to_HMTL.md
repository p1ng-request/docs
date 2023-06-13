<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Microsoft%20Word/Microsoft_Word_Convert_to_HMTL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Microsoft+Word+-+Convert+to+HMTL:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #microsoftword #word #microsoft #html #snippet #operations

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to convert Microsoft Word documents into HTML format.

## Input

### Import library


```python
try:
    import mammoth
except:
    !pip install mammoth
    import mammoth
```

## Model

### Reading file and converting


```python
with open("naas.docx", "rb") as docx_file:
    result = mammoth.convert_to_html(docx_file)
    html = result.value  # The generated HTML
    messages = result.messages  # Any messages, such as warnings during conversion
```

## Output

### Converted


```python
html
```
