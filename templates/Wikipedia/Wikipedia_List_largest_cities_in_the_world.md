<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Wikipedia/Wikipedia_List_largest_cities_in_the_world.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Wikipedia+-+List+largest+cities+in+the+world:+Error+short+description">Bug report</a>

**Tags:** #wikipedia #list #cities #largest #world #data

**Author:** [Florent Ravenel](http://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to extract the list of the largest cities in the world using pandas.read_html() on Wikipedia.

**References:**
- [List of cities by population](https://en.wikipedia.org/wiki/List_of_cities_by_population)

## Input

### Import libraries


```python
import pandas as pd
```

### Setup Variables
- `url`: URL of the Wikipedia page containing the list of cities by population


```python
# Inputs
url = "https://en.wikipedia.org/wiki/List_of_cities_by_population"
```

## Model

### Extract table


```python
df_table = pd.read_html(url)[1]
print('Rows fetched:', len(df_table))
```

### Clean table


```python
df_clean = df_table.copy()

# Dropna
df_clean = df_clean.dropna()

# # Flattern MultiIndex columns
# df_clean.columns = df_clean.columns.get_level_values(1)

print('Cities fetched:', len(df_clean))
df_clean.head(5)
```

## Output

### Display result


```python
df_clean.head(5)
```

 
