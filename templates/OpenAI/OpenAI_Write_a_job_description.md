    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Write_a_job_description.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Write+a+job+description:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #jobdescription #writing #hiring #recruiting #position

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides a guide to write a job description for a specific position for your company.

**References:**
- [Writing a Job Description: A Template to Get You Started](https://www.indeed.com/hire/how-to-write-a-job-description)

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
- `position`: name of the position to write a job description for
- `company`: name of the company recruiting


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
position = "Data Scientist"
company = "naas.ai"
details = "Flexible hours, remote"
prompt = f"Write a job description about '{position}' for '{company}' with specific details: {details}"

# Outputs
file_path = f"Job_description_{position.replace(' ', '_')}_{company}.txt"
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

 
