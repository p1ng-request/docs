<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/XGBoost/XGBoost_Binary_classification_example_with_hyper-parameters_optimization.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=XGBoost+-+Binary+classification+example+with+hyper-parameters+optimization:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #xgboost #snippet #classification #tabular #cross-validation #optimization #modeling

**Author:** [Oussama El Bahaoui](https://www.linkedin.com/in/oelbahaoui/)

**Description:** This notebook provides an example of using XGBoost to perform binary classification with hyper-parameter optimization.

## Input

### Install required packages


```python
%pip install xgboost
```

### Import packages


```python
import pandas as pd

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.model_selection import GridSearchCV
from sklearn.metrics import accuracy_score

from xgboost import XGBClassifier
```

### Variables

Define a parameter grid that will be explored during the hyper-parameters optimization.


```python
# Random seed.
SEED = 42

# A parameters grid for XGBoost classifier.
PARAMS = {
    "objective": ["binary:logistic"],
    "nthread": [-1],
    "random_state": [SEED],
    "min_child_weight": [1, 5, 10],
    "max_depth": [3, 4, 5],
    "learning_rate": [0.01, 0.02, 0.3],
    "n_estimators": [100, 200, 500],
}
```

### Read the dataset


```python
# Load a toy dataset for binary classification task.

data = load_breast_cancer(as_frame=True)
```

## Model

### Create input features and labels


```python
X = data["data"]
y = data["target"]
```

### Split the dataset into train and test sets


```python
# Use 70% of the data for training and 30% for testing.

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=SEED
)
```

### Create a model


```python
# Create a XGBoost classifier model.

model = XGBClassifier()
```

### Optimize the model's hyper-parameters using grid search

A good practice is to perform a [cross-validation training](https://scikit-learn.org/stable/modules/cross_validation.html).

3 or 5-folds are the most recommended values. But to run the notebook faster, we'll reduce it to 2.


```python
# Perfom a grid search on the hyper-parameters defined in the PARAM dict.

grid_search = GridSearchCV(
    estimator=model,
    param_grid=PARAMS,
    scoring="accuracy",
    n_jobs=-1,
    cv=2,
    verbose=True,
).fit(X_train, y_train)
```

Note that the training above takes about 2min to finish. Increasing the number of CV folds will also increase the execution time.

## Output

### Calculate accuracy on test data


```python
# Evaluate on the test data.

y_pred = grid_search.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
```

### Find the best parameters


```python
grid_search.best_params_
```

### Save the model


```python
# Recreate the model using the best hyper-parameters.

best_model = XGBClassifier(**grid_search.best_params_).fit(X_train, y_train)
```


```python
# Saving the model as a json file.

best_model.save_model("best_model.json")
```

### (Optional) Load the model


```python
from xgboost import Booster, DMatrix

trained_model = XGBClassifier()
trained_model.load_model("best_model.json")
```
