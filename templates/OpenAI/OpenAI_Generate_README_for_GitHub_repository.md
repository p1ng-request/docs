<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_README_for_GitHub_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+README+for+GitHub+repository:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #github #readme #repository #generate #automation

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will generate a README for a GitHub repository based on the project name and description.

**References:**
- [GitHub Documentation](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-readme)
- [OpenAI Documentation](https://openai.com/docs/)

## Input

### Import libraries


```python
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai
import naas
```

### Setup Variables
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `project_name`: The name of your project, which should be clear and concise.
- `project_description`: A brief description of your project that explains what it does, why it is important, and how it can be used.


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
project_name = "Naas - Data Product Framework"
project_description = "This data product is a framework to show how to leverage GitHub and naas to build data products in no time."
prompt = f"Write a README file using the best practice of GitHub for this project '{project_name}': '{project_description}'"
```

## Model

### Generate README
Generate a README for a GitHub repository based on the project name and description.


```python
openai.api_key = api_key
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=prompt,
    max_tokens=2084,
    temperature=0.5,
    top_p=0.9
)
```

## Output

### Get text


```python
text = response['choices'][0]['text']
print(text)
```
