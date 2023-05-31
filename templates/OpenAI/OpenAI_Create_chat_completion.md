<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Create_chat_completion.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Create+chat+completion:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #chat #completion #model #response #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates a model response for the given chat conversation. It uses OpenAI's API to generate a response based on the conversation context. This is useful for organizations that need to generate automated responses to customer inquiries.

**References:**
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference/chat/create?lang=python)
- [OpenAI Documentation](https://openai.com/docs/)

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

### Setup Variables
- `api_key`: OpenAI API key. [Get your API key here](https://openai.com/docs/api-overview/).
- `model`: ID of the model to use. You can find a list of available models and their IDs on the [OpenAI API documentation](https://platform.openai.com/docs/models/overview).
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output.
- `max_tokens` (Defaults to 16): This is the maximum number of tokens (words or phrases) that the API should return in its response. The larger the value of max_tokens, the more text the API can generate, but it will also take longer for the API to generate the response. The token count of your prompt plus max_tokens cannot exceed the model's context length. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).
- `messages_role`: The role of the author of this message. One of system, user, or assistant.
- `messages_system`: The contents of the message.
- `messages`: A list of messages describing the conversation so far.


```python
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
model = "gpt-3.5-turbo"
temperature = 0.9
max_tokens = 2084
messages_role = "system"
messages_system = f"""
Act as a chef whose name is Florent. 
Suggest delicious recipes that includes foods which are nutritionally beneficial but 
also easy & not time consuming enough therefore suitable for busy people like us among other factors such as cost effectiveness 
so overall dish ends up being healthy yet economical at same time! 
In your first message, you will present yourself and what you can do.
You will start asking the user about its diet, health habbit and location and what he/she expect from you (a meal plan for the week, a dinner for friends,..) with questions in bullet point.
"""
messages = [
    {"role": messages_role, "content": messages_system}
]
```

## Model

### Send requests to OpenAI API


```python
# Connect with API key
openai.api_key = api_key

# Create chat completion
completion = openai.ChatCompletion.create(
    model=model,
    messages=messages
)
```

## Output

### Display result


```python
print(completion.choices[0].message.content)
```
