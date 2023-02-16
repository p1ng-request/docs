<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Create_Completion.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Create+Completion:+Error+short+description">Bug report</a>

**Tags:** #openai #gpt3 #textcompletion #ai #machinelearning #deeplearning #nlp #datascience #artificialintelligence #tech #innovation #creativity

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook guides you through the process of using OpenAI's Generative Pretrained Transformer 3 (GPT-3) model to build a text completion application. This notebook will show you how to fine-tune GPT-3 to generate text based on a given prompt, and then integrate it into a web application for easy usage. The end result will be a working text completion tool that can be used to generate new ideas, suggestions, or even entire texts with just a few inputs.

<u>References:</u>
- OpenAI API Documentation: https://platform.openai.com/docs/api-reference
- GPT-3: https://openai.com/gpt-3/
- Text Completion with Deep Learning: https://towardsdatascience.com/text-completion-with-deep-learning-4cce287eb716
- Generative Pretrained Transformer 3 (GPT-3) Explained: https://towardsdatascience.com/gpt-3-explained-8bb5f9c0efc7
- A Beginner's Guide to Generative Pre-trained Transformer 3 (GPT-3): https://towardsdatascience.com/a-beginners-guide-to-gpt-3-7d2a3dd3f9e6

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
- [Generate Your API Key](https://elephas.app/blog/how-to-create-openai-api-keys-cl5c4f21d281431po7k8fgyol0)
- `model`: ID of the model to use. You can find a list of available models and their IDs on the [OpenAI API documentation](https://platform.openai.com/docs/models/overview).
- `prompt`: This is the text prompt that you want to send to the OpenAI API.
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output.
- `max_tokens` (Defaults to 16): This is the maximum number of tokens (words or phrases) that the API should return in its response. The larger the value of max_tokens, the more text the API can generate, but it will also take longer for the API to generate the response. The token count of your prompt plus max_tokens cannot exceed the model's context length. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).


```python
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
model = "text-davinci-003"
prompt = "What is OpenAI?"
temperature = 0.6
max_tokens = 2084
```

## Model

### Send requests to OpenAI API


```python
# Connect with API key
openai.api_key = api_key

# Create completion
response = openai.Completion.create(
    model=model,
    prompt=prompt,
    temperature=temperature,
    max_tokens=max_tokens,
)
```

## Output

### Get generated text


```python
# Extract the generated text
text = response["choices"][0]["text"].strip()

# Print the generated text
print("Generated text: ", text)
```
