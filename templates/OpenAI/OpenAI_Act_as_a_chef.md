<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Act_as_a_chef.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a>  <a href="https://workspace.naas.ai/chat/use?plugin_url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Act_as_a_chef.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_MyChatGPT.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Act+as+a+chef:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #chef #cooking #ai #machinelearning #deeplearning

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will create a plugin to act as a chef and use OpenAI to create delicious recipes.

**References:**
- [OpenAI Documentation](https://openai.com/docs/)
- [Awesome ChatGPT Prompts](https://github.com/f/awesome-chatgpt-prompts#act-as-a-chef)

## Input

### Import libraries


```python
import json
import naas
```

### Setup Variables
- `name`: Plugin name to be displayed on naas.
- `model`: ID of the model to use. You can find a list of available models and their IDs on the [OpenAI API documentation](https://platform.openai.com/docs/models/overview).
- `prompt`: This is the text prompt that you want to send to the OpenAI API.
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output.
- `max_tokens` (Defaults to 16): This is the maximum number of tokens (words or phrases) that the API should return in its response. The larger the value of max_tokens, the more text the API can generate, but it will also take longer for the API to generate the response. The token count of your prompt plus max_tokens cannot exceed the model's context length. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).
- `json_path`: json file path to be saved


```python
# Inputs
name = "Act as a chef"
model = "gpt-4"
prompt = f"""
Act as a chef whose name is Florent. 
Suggest delicious recipes that includes foods which are nutritionally beneficial but 
also easy & not time consuming enough therefore suitable for busy people like us among other factors such as cost effectiveness 
so overall dish ends up being healthy yet economical at same time! 
In your first message, you will present yourself and what you can do.
You will start asking the user about its diet, health habbit and location and what he/she expect from you (a meal plan for the week, a dinner for friends,..) with questions in bullet point.
"""
temperature = 1
max_tokens = 2084

# Outputs
json_path = name.lower().replace(" ", "_") + ".json"
```

## Model

### Create plugin


```python
data = {
    "name": name,
    "prompt": prompt.replace("\n", ""),
    "model": model,
    "temperature": temperature,
    "max_tokens": max_tokens,
}
print(json.dumps(data))
```

    {"name": "Act as a chef", "prompt": "Act as a chef whose name is Florent. Suggest delicious recipes that includes foods which are nutritionally beneficial but also easy & not time consuming enough therefore suitable for busy people like us among other factors such as cost effectiveness so overall dish ends up being healthy yet economical at same time! In your first message, you will present yourself and what you can do.You will start asking the user about its diet, health habbit and location and what he/she expect from you (a meal plan for the week, a dinner for friends,..) with questions in bullet point.", "model": "gpt-4", "temperature": 0.9, "max_tokens": 2084}


## Output

### Save json


```python
with open(json_path, "w") as f:
    json.dump(data, f)
```

### Create naas asset


```python
asset_link = naas.asset.add(json_path, params={"inline": True})
```
