<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Save_json_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Save+json+file:+Error+short+description">Bug report</a>

**Tags:** #python #json #file #save #data #io

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will demonstrate how to save a json file using Python.

**References:**
- [Python json module](https://docs.python.org/3/library/json.html)
- [Python json.dump()](https://www.programiz.com/python-programming/methods/json/dump)

## Input

### Import libraries


```python
import json
```

### Setup Variables
- `data`: a dictionary containing the data to be saved in the json file


```python
data = {"name": "John Doe", "age": 30, "city": "New York"}
```

## Model

### Save json file

Using the `json.dump()` function, the `data` dictionary can be saved to a json file.


```python
with open("data.json", "w") as f:
    json.dump(data, f)
```

## Output

### Display result

The json file has been saved to the current directory.

 

 
