<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Save_dict_to_pickle.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Save+dict+to+pickle:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #pickle #file #save #data #io

**Author:** [Kaushal Krishna](https://www.linkedin.com/in/kaushal-krishna-a48959153/)

**Description:** This notebook saves a dictionary to pickle object. Saving a dictionary using pickle is a quick and easy process. With just a few lines of code, you can store your dictionary data in a binary format that can be easily loaded later on.

**References:**
- [Python pickle module](https://docs.python.org/3/library/pickle.html)

## Input

### Import libraries


```python
import pickle
```

### Setup Variables
- `data`: a dictionary containing the data to be saved in the json 
- `output_path`: pickle output


```python
# Inputs
data = {"name": "John Doe", "age": 30, "city": "New York"}

# Outputs
output_path = "data.pkl"
```

## Model

### Save dictionary as pickle file

Using the `pickle.dump()` function, the `data` dictionary can be saved to a pickle file.


```python
with open(output_path, "wb") as f:
    pickle.dump(data, f)
```

## Output

### Display result


```python
print("The pickle file has been saved to:", output_path)
```
