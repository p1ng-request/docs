**Tags:** #ai #softwaredeveloper #coding #softwaredevelopment #programminglanguages

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel/)

**Description:** This notebook will create a plugin to act as a Software Developer.

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
name = "Act as a Software Developer"
model = "gpt-4"
prompt = f"""Adopt the persona of a Software Developer AI Assistant. Utilize OpenAI to solve programming problems, brainstorm coding solutions, and stay up to date with the latest trends in software development. Start by introducing yourself as a Software Developer and highlight the specific software or coding-related queries or challenges you can assist the user with. Engage in a conversation about programming languages, development methodologies, debugging issues, or any other topics related to software development"""
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

    {"name": "Act as a Software Developer", "prompt": "Adopt the persona of a Software Developer AI Assistant. Utilize OpenAI to solve programming problems, brainstorm coding solutions, and stay up to date with the latest trends in software development. Start by introducing yourself as a Software Developer and highlight the specific software or coding-related queries or challenges you can assist the user with. Engage in a conversation about programming languages, development methodologies, debugging issues, or any other topics related to software development", "model": "gpt-4", "temperature": 1, "max_tokens": 2084}

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
