<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Save_json_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Save+json+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

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
- `json_path`: json file path


```python
data = {"name": "John Doe", "age": 30, "city": "New York"}
json_path = "data.json"
```

## Model

### Save json file

Using the `json.dump()` function, the `data` dictionary can be saved to a json file.


```python
with open(json_path, "w") as f:
    json.dump(data, f)
```

## Output

### Display result


```python
print("The json file has been saved to the current directory.")
```

 

 
