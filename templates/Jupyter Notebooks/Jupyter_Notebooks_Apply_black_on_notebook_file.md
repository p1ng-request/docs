<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Jupyter%20Notebooks/Jupyter_Notebooks_Apply_black_on_notebook_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Jupyter+Notebooks+-+Apply+black+on+notebook+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #jupyter #notebook #black #python #formatting #style

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to apply the black formatting style to a Jupyter Notebook file. It is usefull for organizations that want to ensure a consistent coding style across their notebooks.

**References:**
- [Black Vercel](https://black.vercel.app/)
- [Why formatting your python code is important](https://www.freecodecamp.org/news/auto-format-your-python-code-with-black/)

## Input

### Import libraries


```python
import json
import subprocess
```

### Setup Variables
- `file_path`: Path of the Jupyter Notebook file to be formatted


```python
file_path = "<your_notebook_path.ipynb>"
```

## Model

### Apply black formatting


```python
def run_black(file, file_output=None):
    # Open notebook
    with open(file) as f:
        nb = json.load(f)
    
    # Apply black on code cell
    for cell in nb['cells']:
        if cell['cell_type'] == 'code':
            code = cell['source']
            code = "".join(code)
            result = subprocess.run(['black', '-', '--fast'], input=code.encode(), stdout=subprocess.PIPE, stderr=subprocess.PIPE)
            if result.stdout:
                new_code = result.stdout.decode()
                if new_code.endswith("\n"):
                    new_code = new_code[:-1]
                cell['source'] = new_code
                
    # Save notebook
    if not file_output:
        file_output = file
    with open(file_output, 'w') as f:
        json.dump(nb, f, indent=1)
    print(f"✅ Black successfully applied to your notebook.")
```

## Output

### Run function


```python
run_black(file_path)
```

 
