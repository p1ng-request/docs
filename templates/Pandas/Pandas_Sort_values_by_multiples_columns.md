**Tags:** #pandas #dataframe #sort #columns #values #multiples

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook will show how to sort values by multiples columns in Pandas. It is usefull for data analysis and data manipulation.

**References:**
- [Pandas - Sort values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html)
- [Pandas - Tutoriel Sort Value](https://www.geeksforgeeks.org/python-pandas-dataframe-sort_values-set-2/)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables

- `by`: Name or list of names to sort by.
- `ascending`: bool or list of bool, default True. Specify list for multiple sort orders. If this is a list of bools, must match the length of the by.
- `ignore_index`: bool, default False. If True, the resulting axis will be labeled 0, 1, …, n - 1.


```python
by = ['Score', 'Age']
ascending = [False, True]
ignore_index = True
```

## Model

### Create a dataframe


```python
# Create a dataframe
data = {
    "Name": ["Tom", "nick", "krish", "jack"],
    "Age": [20, 21, 19, 18],
    "Score": [99, 98, 95, 90],
}
df = pd.DataFrame(data)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>20</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nick</td>
      <td>21</td>
      <td>98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>krish</td>
      <td>19</td>
      <td>95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>jack</td>
      <td>18</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



## Output

### Sort values by multiples columns


```python
# Sort the DataFrame by multiple columns
sorted_df = df.sort_values(by=by, ascending=ascending, ignore_index=ignore_index)
sorted_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>20</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nick</td>
      <td>21</td>
      <td>98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>krish</td>
      <td>19</td>
      <td>95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>jack</td>
      <td>18</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



 
