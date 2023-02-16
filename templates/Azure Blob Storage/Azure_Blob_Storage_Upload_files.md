<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Azure%20Blob%20Storage/Azure_Blob_Storage_Upload_files.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Azure+Blob+Storage+-+Upload+files:+Error+short+description">Bug report</a>

**Tags:** #azure #datalake #naas #snippet

**Author:** [Alexandre Stevens](https://www.linkedin.com/in/) <br>

**Description:** This notebook explains how to upload files to Azure Blob Storage using the Azure Python SDK.

## Input

### Import libraries
In order to update a file into Azure blob storage in Python, you will need to use the Azure Storage SDK for Python.


```python
try:
    from azure.storage.blob import BlobServiceClient
    from azure.storage.blob import ContentSettings
except ImportError:
    !pip install azure-storage-blob --user
    !pip install azure-keyvault-secrets --user
    !pip install azure-mgmt-resource --user
    !pip install azure-mgmt-storage --user
    !pip install azure-mgmt-compute --user
    from azure.storage.blob import BlobServiceClient
    from azure.storage.blob import ContentSettings
```

### Setup Variables
- ACCOUNT_URL: Your account url in azure blob storage, example: 'https://yourproject.blob.core.windows.net'
- KEY_ACCOUNT: Your Azure credentials, To get access please follow the procedure [here](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)
- CONTAINER_NAME: Container name in your Azure project where files will be store
- FILE_NAME: Name of the file in your container
- UPLOAD_FILE_PATH: File to be uploaded


```python
# Connect to your storage account
ACCOUNT_URL = "https://yourproject.blob.core.windows.net"
KEY_ACCOUNT = "########"
CONTAINER_NAME = "container_name"
FILE_NAME = "file_name.csv"

# File to be uploaded
UPLOAD_FILE_PATH = "../outputs/filename.csv"
```

## Model

### Create a BlobServiceClient using the connection string


```python
# Create a BlobServiceClient using the connection string
blob_service_client = BlobServiceClient(account_url=ACCOUNT_URL, credential=KEY_ACCOUNT)
```

### Create a ContainerClient


```python
# Create a ContainerClient
blob_client = blob_service_client.get_blob_client(
    container=CONTAINER_NAME, blob=FILE_NAME
)
```

## Output

### Upload the file to the container


```python
with open(file=UPLOAD_FILE_PATH, mode="rb") as data:
    blob_client.upload_blob(data, overwrite=True)
print("File has been uploaded to Azure Blob Storage")
```
