<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_Act_as_a_x_notebook.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate_Act_as_a_x_notebook:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #ai #machinelearning #deeplearning #notebooks #automation #gsheet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook creates "Act as a ..." notebooks from a Google Sheets spreadsheet using OpenAI_Act_as_a_chef.ipynb as template.

**References:**
- [OpenAI Documentation](https://openai.com/docs/)
- [Awesome ChatGPT Prompts](https://github.com/f/awesome-chatgpt-prompts#act-as-a-chef)

## Input

### Import libraries


```python
from papermill.iorw import (
    load_notebook_node,
    write_ipynb,
)
import naas
from naas_drivers import gsheet
import copy
import json
import subprocess
```

### Setup Variables


```python
# Inputs
spreadsheet_url = "https://docs.google.com/spreadsheets/d/"
sheet_name = "Templates"

# Outputs
notebook_init = "OpenAI_Act_as_a_chef.ipynb"
name_init = "Act as a chef"
model = "gpt-4"
prompt_init = f"""
Act as a chef whose name is Florent. 
Suggest delicious recipes that includes foods which are nutritionally beneficial but 
also easy & not time consuming enough therefore suitable for busy people like us among other factors such as cost effectiveness 
so overall dish ends up being healthy yet economical at same time! 
In your first message, you will present yourself and what you can do.
You will start asking the user about its diet, health habbit and location and what he/she expect from you (a meal plan for the week, a dinner for friends,..) with questions in bullet point.
"""
temperature = 1
max_tokens = 2084
```

## Model

### Open template notebook


```python
# Get notebook
nb_init = load_notebook_node(notebook_init)
```

### Get data from Google Sheets spreadsheet


```python
df_input = gsheet.connect(spreadsheet_url).get(sheet_name=sheet_name)
print("Row fetched:", len(df_input))
df_input.head(1)
```

## Output

### Create notebooks


```python
for row in df_input.itertuples():
    # Init
    nb = copy.deepcopy(nb_init)
    name = row.Name
    description = row.Description
    tags = row.Tags
    prompt = row.Prompt
    
    # Prep outputs
    notebook_output = f"OpenAI_{name.replace(' ', '_')}.ipynb"
    title = f"# OpenAI - {name}"
    hashtags = f"**Tags:** {tags.lower()}"
    author = "**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel/)"
    nb_description = f"**Description:** {description}"
    variables = nb.cells[10].source
    data = {
        "name": name,
        "prompt": prompt.replace("\n", ""),
        "model": model,
        "temperature": temperature,
        "max_tokens": max_tokens,
    }
    
    # Update notebook
    nb.cells[1].source = title
    nb.cells[2].source = hashtags
    nb.cells[3].source = author
    nb.cells[4].source = nb_description
    nb.cells[10].source = variables.replace(name_init, name, 1).replace(prompt_init, prompt)
    nb.cells[13].outputs[0]["text"] = json.dumps(data)
    
    # Save new notebook
    write_ipynb(nb, notebook_output)
```
