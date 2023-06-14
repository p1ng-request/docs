<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Deepl/Deepl_Translated_string_to_txt.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Deepl+-+Translated+string+to+txt:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #deepl #translate #text #txt #api #string

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook show how to translate a string with Deepl API and save it in a txt file.

**References:**
- [Deepl API docs](https://www.deepl.com/docs-api)
- [Languages Codes](https://www.deepl.com/docs-api/translate-text)

## Input

### Import libraries


```python
import naas
try:
    import deepl
except:
    !pip install deepl --user
    import deepl
```

### Setup Variables
[Get your authentification key](https://github.com/Benjifilly/My_notebooks/wiki)
- `auth_key`: The auth key is a unique identifier used for authentication and access to the DeepL API. It ensures that only authorized users can make API requests.
- `text`: the text to be translated
- `target_lang`: the language you wish to translate into, for more languages, go to references
- `output_file_path`: the directory where you want to save the file if you are using Naas it will start with `home/ftp/`


```python
auth_key = naas.secret.get("DEEPL_AUTH_KEY") or 'YOUR_DEEPL_AUTH_KEY'  # Replace with your actual DeepL API authentication key
text = '''
Announcing the Python client library for the DeepL API
August 16, 2021
We’re excited to announce the release of our Python client library for the DeepL API. This is the first programming language-specific library we’ve built for the API, and our goal is to make it much easier for developers working with Python to build applications with DeepL.
'''
target_lang = 'fr'  # French
output_file_path = "/home/ftp/file.txt"  
```

## Model

### Translate the text


```python
translator = deepl.Translator(auth_key)
result = translator.translate_text(text, target_lang=target_lang)
translated_text = result.text
```

### Save translated text to a text file


```python
with open(output_file_path, 'w', encoding='utf-8') as file:
    file.write(translated_text)
```

## Output

### Display result


```python
print("Text file generated successfully here ->", output_file_path)
print("------------------------------------------------------------")
print("Result:")
print(translated_text)
```
