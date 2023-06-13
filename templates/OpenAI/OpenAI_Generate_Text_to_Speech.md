<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_Text_to_Speech.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+Text+to+Speech:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai

**Author:** [Sriniketh Jayasendil](http://linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook focusses on using OpenAI for text-to-speech generation using [gTTS](https://pypi.org/project/gTTS/)

## Input

### Import libraries


```python
import os
import naas

# OpenAI
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai

# Google Text to Speech API
try:
    from gtts import gTTS
except ModuleNotFoundError:
    !pip install --user gTTS
    from gtts import gTTS
```

### Setup Variables


```python
# Inputs
openai.api_key = naas.secret.get("OPENAI_API_KEY") or "OPENAI_API_KEY"
language = 'en'
prompt = input('Enter the prompt: ')

# Outputs
speech_output = ''
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
  presence_penalty=0.0,
  stop=["\"\"\""]
)

speech_output = gTTS(text=response.choices[0].text, lang=language, slow=True)
```

## Output

### Save audio in `.mp3` format


```python
speech_output.save('output.mp3')
```
