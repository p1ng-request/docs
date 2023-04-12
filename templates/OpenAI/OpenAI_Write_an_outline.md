    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Write_an_outline.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Write+an+outline:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #outline #writing #topic #structure #organize

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will provide an outline for writing a specific topic. An outline is a structured plan or framework that serves as a blueprint for organizing and presenting information in a clear and logical way. Outlines can be used for a variety of purposes, such as organizing an essay or research paper, preparing a speech or presentation, or planning a project.

**References:**
- [Writing an Outline](https://www.wikihow.com/Write-an-Outline)
- [Outline Structure](https://www.scribbr.com/academic-writing/outline/)

## Input

### Import Libraries


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
- `topic`: the topic to be written about
- `subtopics`: a list of subtopics related to the main topic


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
topic = "OpenAI"
subtopics = "GPT-3, Reinforcement Learning, Generative Models"
prompt = f"Write an outline about '{topic}' with this subtopics '{subtopics}' and references and citations at the end."

# Outputs
file_path = f"Outline_{topic.replace(' ', '_')}.txt"
```

## Model

### Send requests to OpenAI API


```python
openai.api_key = api_key
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=prompt,
    max_tokens=2048,
    temperature=0.5,
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
