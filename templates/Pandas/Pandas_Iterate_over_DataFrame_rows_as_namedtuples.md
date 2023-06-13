<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Iterate_over_DataFrame_rows_as_namedtuples.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Iterate+over+DataFrame+rows+as+namedtuples:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #pandas #python #loops #snippet #operations #namedtuples #dataframe

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook demonstrates how to iterate over DataFrame rows as namedtuples

**References:**
- [Pandas - DataFrame.itertuples](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.itertuples.html)
- [Numpy - random.choice](https://numpy.org/doc/stable/reference/random/generated/numpy.random.choice.html)
- [Collections - namedtuple](https://www.geeksforgeeks.org/namedtuple-in-python/)

## Input

### Import libraries


```python
import pandas as pd
import numpy as np
from collections import namedtuple
```

## Model

### Create Sample Dataframe 


```python
dict1 = {
    "student_id": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], # List of student IDs
    "student_name": [
        "Peter",
        "Dolly",
        "Maggie",
        "David",
        "Isabelle",
        "Harry",
        "Akin",
        "Abbey",
        "Victoria",
        "Sam",
    ], # List of student names
    "student_course": np.random.choice(["Biology", "Physics", "Chemistry"], size=10), # List of random courses for each student
}

# DataFrame creation from the dictionary
df = pd.DataFrame(dict1)
df
```

### Definition of namedtuple


```python
# Creation of a namedtuple called "Student" with "index" fields and df DataFrame columns
Student = namedtuple("Student", ["index"] + df.columns.tolist())
```

## Output

### Display result


```python
for row in df.itertuples(index=True, name="Student"):# Iteration on df DataFrame rows using itertuples
    student = Student(*row) # Create a Student object from each line
    print("Index:", student.index) # Display student information
    print("Student ID:", student.student_id)
    print("Name:", student.student_name)
    print("Course:", student.student_course)
    print()
```


```python

```
