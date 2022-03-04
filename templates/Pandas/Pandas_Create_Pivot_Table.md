<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Pandas - Create Pivot Table
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Pandas/Pandas_Create_Pivot_Table.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #pandas #pivot

## Input

### Import library


```python
import pandas as pd
```

### Variables


```python
df = pd.DataFrame(
    {
        "item": ["apple", "apple", "apple", "apple", "apple"],
        "size": ["small", "small", "large", "large", "large"],
        "location": ["Walmart", "Aldi", "Walmart", "Aldi", "Aldi"],
        "price": [3, 2, 4, 3, 2.5],
    }
)
df
```

## Model

### Function


```python
pivot = pd.pivot_table(
    df, values="price", index=["item", "size"], columns=["location"], aggfunc="mean"
)
```

## Output

### Display result


```python
pivot
```
