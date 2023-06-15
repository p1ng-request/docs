<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Algolia/Algolia_List%20indices.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Algolia+-+List+indices:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #algolia #python #api #index #list

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to get a list of indices with their associated metadata from Algolia using Python. This method retrieves a list of all indices associated with a given Application ID.
The returned list includes the names of the indices as well as their associated metadata, such as the number of records, size, and last build time.

**References:**
- [Algolia API Reference](https://www.algolia.com/doc/api-reference/api-methods/list-indices/)
- [Algolia Python Client](https://github.com/algolia/algoliasearch-client-python)

## Input

### Import libraries


```python
try:
    from algoliasearch.search_client import SearchClient
except:
    !pip install algoliasearch --user
    from algoliasearch.search_client import SearchClient
import naas
```

### Setup Variables
- `app_id`: Algolia application ID. [Get your credentials](https://dashboard.algolia.com/account/api-keyss)
- `api_key`: Algolia API key. [Get your credentials](https://dashboard.algolia.com/account/api-keys)


```python
app_id = naas.secret.get("ALGOLIA_APP_ID") or "<YOUR_APP_ID>"
api_key = naas.secret.get("ALGOLIA_API_KEY") or "<YOUR_API_KEY>"
```

## Model

### Connect to Algolia


```python
# Initialize the Algolia client
client = SearchClient.create(app_id, api_key)
```

### List indices


```python
indices = client.list_indices()
indices
```

## Output

### Display outputs


```python
print("Indices fetched:", len(indices.get("items")))
indices.get("items")
```
