<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Algolia/Algolia_Add_or_Replace_all_attributes_in_single_record.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Algolia+-+Add+or+Replace+all+attributes+in+a+single+record:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #algolia #python #api #index #object #save #update #add

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to add new record (object) to an index or replace existing record with an updated set of attributes.
This method redefines all of a record’s attributes (except its objectID). In other words, it fully replaces an existing record.

**References:**
- [Algolia API Reference](https://www.algolia.com/doc/api-reference/api-methods/save-objects/)
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
- `single_object`: An dict with keys and values to be added or updated in the Algolia index. This dict must contain a unique identifier field called "objectID". If the "objectID" field is not present, Algolia will automatically generate a new unique identifier for the object.


```python
app_id = naas.secret.get("ALGOLIA_APP_ID") or "<YOUR_APP_ID>"
api_key = naas.secret.get("ALGOLIA_API_KEY") or "<YOUR_API_KEY>"
index_name = "<YOUR_INDEX_NAME>"
single_object = {'firstname': 'Jimmie', 'lastname': 'Barninger', 'objectID': 'myID1'},
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

### Add or Replace all attributes in a single record


```python
index.save_object(single_object)
```
