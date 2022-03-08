<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Microsoft%20Word/Microsoft_Word_Convert_to_HMTL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #word #microsoft

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

## Input

### Install package


```python
!pip install mammoth
```

### Import library


```python
import mammoth
```

## Model

### Reading file and converting


```python
with open("naas.docx", "rb") as docx_file:
    result = mammoth.convert_to_html(docx_file)
    html = result.value # The generated HTML
    messages = result.messages # Any messages, such as warnings during conversion
```

## Output

### Converted


```python
html
```
