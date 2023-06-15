<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Algolia/Algolia_Delete_single_object.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Algolia+-+Delete+a+single+object:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #algolia #python #api #index #object #delete

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to delete a single object from an Algolia index using Python.

**References:**
- [Algolia API Reference](https://www.algolia.com/doc/api-reference/api-methods/delete-objects/)
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
- `index_name`: Algolia index name
- `object_id`: Object id to be deleted


```python
app_id = naas.secret.get("ALGOLIA_APP_ID") or "<YOUR_APP_ID>"
api_key = naas.secret.get("ALGOLIA_API_KEY") or "<YOUR_API_KEY>"
index_name = "<YOUR_INDEX_NAME>"
object_id = 'ff7e6a98c0dbf_dashboard_generated_id'
```

## Model

### Connect to Algolia and initialize index


```python
# Initialize the Algolia client
client = SearchClient.create(app_id, api_key)

# Initialize the Algolia index
index = client.init_index(index_name)
```

## Output

### Delete single object


```python
index.delete_object(object_id)
```
