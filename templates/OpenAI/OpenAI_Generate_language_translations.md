<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_language_translations.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+language+translations:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #language #translation #ai #translator #operations #snippet

**Author:** [Minura Punchihewa](https://www.linkedin.com/in/minurapunchihewa/)

**Description:** This notebook translates a given text to a language of choice using OpenAI.

<u>References:</u>
- https://platform.openai.com/docs/api-reference/completions/create
- https://platform.openai.com/docs/models/overview

## Input

### Import libraries


```python
try:
    import openai
except:
    !pip install openai --user
    import openai
import naas
```

### Setup OpenAI
[How to generate your OpenAI API KEY?](https://elephas.app/blog/how-to-create-openai-api-keys-cl5c4f21d281431po7k8fgyol0)


```python
openai.api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
```

### Setup Variables
The value of the `target_language` variable in the code should be a 2-letter ISO 639-1 language code representing the target language you want to translate the text to. Here are some common language codes:
- English: "en"
- Spanish: "es"
- French: "fr"
- German: "de"
- Italian: "it"
- Dutch: "nl"
- Portuguese: "pt"
- Russian: "ru"
- Chinese: "zh"
- Japanese: "ja"
- Korean: "ko"
This list is not exhaustive, and there are many more language codes that you can use. You can find a complete list of ISO 639-1 language codes on the ISO website: https://www.loc.gov/standards/iso639-2/php/code_list.php


```python
text = "What rooms do you have available?"
target_language = "fr"
```

## Model

### Send requests to OpenAI API
- `model`: ID of the model to use. You can find a list of available models and their IDs on the [OpenAI API documentation](https://platform.openai.com/docs/models/overview).
- `prompt`: This is the text prompt that you want to send to the OpenAI API. It specifies the text you want to translate, and the target language you want to translate it to. In the example code, the prompt is constructed by concatenating the target language and the text to be translated.
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output. In the example code, 0.3 is used, which is a common value for this parameter.
- `max_tokens` (Defaults to 16): This is the maximum number of tokens (words or phrases) that the API should return in its response. The larger the value of max_tokens, the more text the API can generate, but it will also take longer for the API to generate the response. The token count of your prompt plus max_tokens cannot exceed the model's context length. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).


```python
# Use the API to translate the text
response = openai.Completion.create(
    model="text-davinci-003",
    prompt=f"Translate this into {target_language}: {text}",
    temperature=0.3,
    max_tokens=100,
)

# Extract the translated text
translated_text = response["choices"][0]["text"].strip()
```

## Output

### Get the translation


```python
# Print the translated text
print("Translated text: ", translated_text)
```


```python

```
