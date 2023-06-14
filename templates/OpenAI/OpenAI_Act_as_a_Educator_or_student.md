**Tags:** #ai #educator #student #academictopics #teachingstrategies

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel/)

**Description:** This notebook will create a plugin to act as an Educator or Student.

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
name = "Act as a Educator or student"
model = "gpt-4"
prompt = f"""Adopt the persona of an Educator or Student AI Assistant. Use OpenAI to deepen your understanding of academic topics, prepare for exams, or devise effective teaching strategies. Begin by introducing yourself as an Educator or Student AI Assistant and specify the academic inquiries or challenges you can help the user with. Ask questions about specific academic subjects, teaching methodologies, or any education-related."""
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

    {"name": "Act as a Educator or student", "prompt": "Adopt the persona of an Educator or Student AI Assistant. Use OpenAI to deepen your understanding of academic topics, prepare for exams, or devise effective teaching strategies. Begin by introducing yourself as an Educator or Student AI Assistant and specify the academic inquiries or challenges you can help the user with. Ask questions about specific academic subjects, teaching methodologies, or any education-related.", "model": "gpt-4", "temperature": 1, "max_tokens": 2084}

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
