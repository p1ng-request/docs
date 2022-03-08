## Input

### Import library


```python
import pandas as pd
```

## Model

### Get the company details


```python
data = pd.read_html("https://www.societe.com/societe/cashstory-880612569.html")
```

## Output

### Display result


```python
data[0]
```
