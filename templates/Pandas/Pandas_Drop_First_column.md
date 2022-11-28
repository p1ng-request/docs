<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Drop_First_column.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Pandas+-+Drop+First+column:+Error+short+description">Bug report</a>

**Tags:** #pandas #snippet #datacleaning #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to drop First Column in Pandas DataFrame (3 Methods).

<u>Reference:</u> https://www.statology.org/pandas-drop-first-column/

## Input

### Import libraries


```python
import pandas as pd
```

### Setup DataFrame


```python
#create DataFrame
df = pd.DataFrame({'team': ['A', 'A', 'A', 'B', 'B', 'B'],
                   'points': [11, 7, 8, 10, 13, 13],
                   'assists': [5, 7, 7, 9, 12, 9],
                   'rebounds': [11, 8, 10, 6, 6, 5]})
df
```

## Model

### Method 1: Use drop
The following code shows how to use the drop() function to drop the first column of the pandas DataFrame.


```python
#Copy init dataframe
df1 = df.copy()

df1 = df1.drop(columns=df1.columns[0], axis=1)
print(f"✅ Column '{df1.columns[0]}' removed from DataFrame.")
df1
```

### Method 2: Use iloc
The following code shows how to use the iloc function to drop the first column of the pandas DataFrame.


```python
#Copy init dataframe
df2 = df.copy()


df2= df2.iloc[: , 1:]
print(f"✅ Column '{df2.columns[0]}' removed from DataFrame.")
df2
```

### Method 3: Use del
The following code shows how to use the del function to drop the first column of the pandas DataFrame.


```python
#Copy init dataframe
df3 = df.copy()

del df3[df3.columns[0]]
print(f"✅ Column '{df3.columns[0]}' removed from DataFrame.")
df3
```

## Output

### Display Result


```python
print("✅ Each method produces the same result")
```
