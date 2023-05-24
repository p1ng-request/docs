<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_text_summaries.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+text+summaries:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #text #summary 

**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook shows how to use the OpenAI API to generate text summaries.

## Input

### Install package


```python
import naas
# OpenAI
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai
```

### Setup Variables
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `text`: Input text that needs to be summarized


```python
# OpenAI API key
openai.api_key = naas.secret.get("OPENAI_API_KEY")

# prompt to get text
text = input('Enter the your text: ')
```


```python
# prompt for model
prompt = "Summarize the given text: " + text
```

## Model

### Establish connection with OpenAI and get the response


```python
# Model to generate the repsonse
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
# Get the summary from response generated
summary = response.choices[0].text
```

## Output


```python
# Display the summary
print(summary)
```
