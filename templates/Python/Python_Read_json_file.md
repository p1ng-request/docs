<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Read_json_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Read+json+file:+Error+short+description">Bug report</a>

**Tags:** #python #json #read #file #data #parse

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will demonstrate how to read a json file in Python.

**References:**
- [Python json module](https://docs.python.org/3/library/json.html)
- [JSON format](https://www.json.org/json-en.html)

## Input

### Import libraries


```python
import json
```

### Setup Variables
- `file_name`: Name of the json file to be read


```python
file_name = "data.json"
```

## Model

### Read json file

This function will read the json file and return the content as a dictionary.


```python
def read_json_file(file_name):
    with open(file_name) as json_file:
        data = json.load(json_file)
    return data
```

## Output

### Display result


```python
data = read_json_file(file_name)
print(data)
```

 
