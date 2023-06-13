<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Read_pickle_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Read+pickle+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #pickle #file #load #data #io

**Author:** [Kaushal Krishna](https://www.linkedin.com/in/kaushal-krishna-a48959153/)

**Description:**   
This notebook loads a dictionary from pickle object. Loading a dictionary using pickle is a quick and easy process. With just a few lines of code, you can store your dictionary data from a pickle file.    

Pickle can cause critical security vulnerabilities in code, you should never unpickle data you don’t trust. If you must accept data from an untrusted client, you should use the safer JSON format. And, if you transfer pickled data between trusted applications but need extra measures to prevent tampering, you should generate an HMAC signature you can verify before unpickling.

**References:**
- [Python pickle module](https://docs.python.org/3/library/pickle.html)

## Input

### Import libraries


```python
import pickle
```

### Setup Variables
- `data`: a variable to store unpickled object
- `input_path`: pickle file source


```python
# Inputs
input_path = "data.pkl"

# Outputs
data = None
```

## Model

### Load dictionary from pickle file

Using the `pickle.load()` function, the `data` dictionary can be loaded into from a pickle file.


```python
with open(input_path, "rb") as f:
    data=pickle.load(f)
```

## Output

### Display result


```python
print("The unpickled object is : \n", data)
```
