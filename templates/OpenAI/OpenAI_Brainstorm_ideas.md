<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Brainstorm_ideas.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Brainstorm+ideas:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #brainstorm #ideas #ai #machinelearning #deeplearning

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will help brainstorm ideas on a specific topic using OpenAI.

**References:**
- [OpenAI](https://openai.com/)
- [Brainstorming](https://en.wikipedia.org/wiki/Brainstorming)

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
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `topic`: the topic to brainstorm ideas on


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
topic = "AI"
prompt = f"Brainstorm ideas on '{topic}'"

# Outputs
file_path = f"Brainstorm_ideas_{topic.replace(' ', '_')}.txt"
```

## Model

### Send requests to OpenAI API


```python
openai.api_key = api_key
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=prompt,
    max_tokens=100,
    temperature=0.9,
)
```

### Get text


```python
text = response['choices'][0]['text']
print(text)
```

## Output

### Save text to txt file


```python
text_file = open(file_path, "w")
text_file.write(text)
text_file.close()
```


```python

```
