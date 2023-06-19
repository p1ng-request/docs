<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Count_tokens_with_tiktoken.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Count+tokens+with+tiktoken:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #tiktoken #count #token #tokens #cookbook

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to count tokens used from a string with tiktoken to use OpenAI API.

**References:**
- [OpenAI Cookbook](https://github.com/openai/openai-cookbook)
- [How to count tokens with tiktoken](https://github.com/openai/openai-cookbook/blob/main/examples/How_to_count_tokens_with_tiktoken.ipynb)

## Input

### Import libraries


```python
try:
    import tiktoken
except:
    !pip install tiktoken --user
    import tiktoken
```

### Setup Variables
- `text_string`: Given text string
- `encoding_name`: Encoding


```python
text_string = "tiktoken is great!"
encoding_name = "cl100k_base"
```

## Model

### Count tokens
Count tokens by counting the length of the list returned by .encode()


```python
def num_tokens_from_string(string: str, encoding_name: str) -> int:
    """Returns the number of tokens in a text string."""
    encoding = tiktoken.get_encoding(encoding_name)
    num_tokens = len(encoding.encode(string))
    return num_tokens
```

## Output

### Display result


```python
num_tokens = num_tokens_from_string(text_string, encoding_name)
print("Tokens:", num_tokens)
```

 
