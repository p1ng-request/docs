<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Transform_DataFrame_to_json_file.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Transform+DataFrame+to+json+file:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #dataframe #json #transform #file #dict #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to transform a DataFrame into a json file. It is usefull for organizations that need to store data in a json format.

**References:**
- [Pandas DataFrame to_dict](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_dict.html)
- [JSON - Wikipedia](https://en.wikipedia.org/wiki/JSON)

## Input

### Import libraries


```python
import pandas as pd
import json
```

### Setup Variables
- `orient` : Determines the type of the values of the dictionary ('dict', 'list', 'series', 'split', 'tight', 'records', 'index')
- `df`: fake DataFrame
- `json_path`: json file path


```python
orient = "records"
df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]})
json_path = "data.json"
```

## Model

### Transform DataFrame to dict



```python
# Transform DataFrame to json
data = df.to_dict(orient=orient)
data
```

## Output

### Save dict to JSON


```python
with open(json_path, "w") as f:
    json.dump(data, f)
print("The json file has been saved to the current directory.")
```

 
