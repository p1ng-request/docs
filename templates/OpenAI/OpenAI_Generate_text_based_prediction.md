    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_text_based_prediction.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+text+based+prediction:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #prediction #text

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook shows how to use the OpenAI API to make predictions based on text data

## Input

### Install package


```python
import os
# OpenAI
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai
```

### Setup Variables


```python
# api key
openai.api_key = "OPENAI_API_KEY"

# prompt to make prediction
prompt = input('Enter the prompt: ')

# Outputs
prediction = ''
```

## Model

### Establish connection with OpenAI and get the response


```python
response = openai.Completion.create(
  model="text-davinci-003",
  prompt=prompt,
  temperature=0.7,
  max_tokens=256,
  top_p=1.0,
  frequency_penalty=0.0,
  presence_penalty=0.0
)
```


```python
# get the prediction from response generated
prediction = response.choices[0].text
```

## Output


```python
print(prediction)
```
