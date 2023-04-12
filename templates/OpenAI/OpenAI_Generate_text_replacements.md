<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_text_replacements.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+text+replacements:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #text_replacement

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook shows how to use the OpenAI API to generate text replacements such as correcting grammatical errors or making text more formal.

## Input


```python
import naas
import os
# OpenAI
try:
    import openai
except ModuleNotFoundError:
    !pip install openai
    import openai
```

### Setup Variables
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `text`: the text to be corrected


```python
# api key
openai.api_key = naas.secret.get("OPENAI_API_KEY")

# prompt for open ai
prompt = 'Correct the grammatical error and make the text formal.\n'

# prompt to enter text to be corrected
text = input('Enter your text:')
```


```python
# complete prompt to be passed to model
complete_prompt = prompt + text
```

## Model

### Establish connection with OpenAI and get the response


```python
response = openai.Completion.create(
  model="text-davinci-003",
  prompt=complete_prompt,
  temperature=0.7,
  max_tokens=256,
  top_p=1.0,
  frequency_penalty=0.0,
  presence_penalty=0.0
)
```


```python
# get the text with replacements from response generated
new_text = response.choices[0].text
```

## Output


```python
#printing the text generated
print(new_text)
```
