<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_Q%26A.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+Q&A:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #q&a 

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook shows how to use the OpenAI API to generate answer to a question.

## Input

### Install package


```python
import naas
import os
# OpenAI
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai
```

### Setup Variables
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `question`: the question to get the answer


```python
# api key
openai.api_key = naas.secret.get("OPENAI_API_KEY")

# prompt to ask question
question = input('Enter the question: ')
```

## Model

### Establish connection with OpenAI and get the response


```python
response = openai.Completion.create(
  model="text-davinci-003",
  prompt=question,
  temperature=0.7,
  max_tokens=256,
  top_p=1.0,
  frequency_penalty=0.0,
  presence_penalty=0.0
)
```


```python
# get the answer from response generated
answer = response.choices[0].text
```

## Output


```python
print(answer)
```
