<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Transform_string_to_Secure_Hash_Algorithm.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Transform+String+to+Secure+Hash+Algorithm:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #security #hash #algorithm #encryption #sha

**Author:** [Firstname LastName](https://www.linkedin.com/in/xxxxxx/)

**Description:** This notebook will demonstrate how to create a secure hash algorithm using Python. It is useful for organizations to ensure data security and integrity.

**References:**
- [Python hashlib](https://docs.python.org/3/library/hashlib.html)
- [Secure Hash Algorithm](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms)

## Input

### Import libraries


```python
try:
    import hashlib
except:
    !pip install hashlib --user
    import hashlib
```

### Setup Variables
- `message`: The message to be hashed


```python
message = "This is a message to be hashed"
```

## Model

### Create SHA-256 Hash

This function will create a SHA-256 hash of the message.


```python
def create_sha_256_hash(message):
    # Encode the message to bytes
    message_bytes = message.encode()

    # Create the hash object
    sha_256_hash = hashlib.sha256(message_bytes)

    # Return the hexadecimal digest of the hash
    return sha_256_hash.hexdigest()
```

## Output

### Display result


```python
print(create_sha_256_hash(message))
```

 
