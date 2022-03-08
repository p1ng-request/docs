This notebook will help you understand how to convert any date to ISO date format.

**Author:** [Oketunji Oludolapo](https://www.linkedin.com/in/oludolapo-oketunji/)

## Input

### Import Libraries


```python
import pandas as pd
from dateutil.parser import parse
```

### Create Sample Dataframe 


```python
dict1 = {
    "Name": ["Peter","Dolly","Maggie","David","Isabelle"],
    "Date":["20/2/2021","19/8/2014","8/9/2000","4/3/2013","14/7/1995"],
    "Second Date":["August 20,2011","September 16,1993","January 23,2009","October 17,2019","March 4,2021"]
}
```


```python
data=pd.DataFrame(dict1)
```


```python
data
```

## Model
ISO date format is the standard internationally acceptable format of writing date. It eliminates the differences between the date format of different regions. This template will convert any date to ISO format. 
There are 2 date formats in the sample data and the conversion of both takes place below


```python
# Converting the first Date into ISO Format 
data["Date"]=pd.to_datetime(data["Date"]).dt.strftime('%Y-%m-%d')
```


```python
# Converting the second date into ISO Format
data["Second Date"]=data["Second Date"].apply(lambda i: parse(i))
```

## Output

### Display result


```python
data
```
