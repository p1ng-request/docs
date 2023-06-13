<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Polars/Polars_Read_CSV.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Polars+-+Read+CSV:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #polars #dataframe #read #python #library #data #csv

**Author:** [Minura Punchihewa](https://www.linkedin.com/in/minurapunchihewa/)

**Description:** This notebook will demonstrate how to read a csv using the Polars library.

About Polars:
- `polars` is a Python library for data manipulation that is built on top of Rust's `Apache Arrow` and `DataFusion` projects.
- It offers fast and efficient data processing and manipulation capabilities for large datasets, with a Pandas-like API and support for advanced data types.
- `polars` is especially useful for data-intensive applications such as machine learning, data analysis, and data visualization, and can handle datasets that are too large to fit into memory.

**References:**
- [Polars](https://pypi.org/project/polars/)
- [Dataframe](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)

## Input

### Import libraries


```python
try:
    import polars as pl
except ModuleNotFoundError:
    !pip install polars
    import polars as pl
```

### Setup Variables
- `file_path`: path of your csv file


```python
# Inputs
file_path = 'https://raw.githubusercontent.com/plotly/datasets/master/2014_us_cities.csv'
```

## Model

### Read dataframe

Read the dataframe using the `read_csv` method.


```python
df = pl.read_csv(file_path)
```

## Output

### Display result


```python
df.head()
```
