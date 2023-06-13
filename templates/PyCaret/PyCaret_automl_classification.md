<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/PyCaret/PyCaret_automl_classification.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=PyCaret+-+Automl+classification:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #automl #pandas #snippet #classification #dataframe #visualize #pycaret #operations

**Author:** [Minura Punchihewa](https://www.linkedin.com/in/minurapunchihewa/)

**Description:** This notebook demonstrates how to use PyCaret to quickly and easily build and evaluate machine learning models for classification tasks.

## Input

### Import libraries


```python
import pandas as pd
try:
    from pycaret.classification import setup, compare_models, evaluate_model, predict_model, finalize_model, \
     save_model, load_model, create_docker
except:
    ! pip install --user pycaret
    from pycaret.classification import setup, compare_models, evaluate_model, predict_model, finalize_model, \
     save_model, load_model, create_docker
    
```

### Variables


```python
csv_path = "https://raw.githubusercontent.com/MinuraPunchihewa/pycaret-automl/main/data/iris.csv"
target_column = "variety"
```

## Model

### Read the CSV from path


```python
df = pd.read_csv(csv_path)
```

### View a sample of the data


```python
df.head()
```

### Setup the dataset


```python
# must be called before executing any other function
# can configure many types of transformation operations
# by default Missing Value Imputation, One-Hot Encoding and Train-Test Split operations will be performed
# press enter to continue
grid = setup(data=df, target=target_column)
```

### Train and compare all supported models


```python
# uses cross-validation
best_model = compare_models()
```

### Report the best model


```python
print(best_model)
```

### Evaluate the model using a number of different plots


```python
# click on the different plot types to exlpore
# some plots may not work depending on the data and the model
evaluate_model(best_model)
```

### Make predictions on new data


```python
# data should be a DataFrame without label
# predict_model(best_model, new_data)
```

### Finalize model


```python
# trains the model on the entire dataset including the hold-out set
# does not change any parameter of the model
final_model = finalize_model(best_model)
```

## Output

### Save model as a pickle file


```python
save_model(final_model, "classification_model")
```

### Load saved model from pickle file


```python
model = load_model("classification_model")
```

### Create Dockerfile for model


```python
# also creates a requirements.txt file for dependencies
create_docker("classification_model")
```
