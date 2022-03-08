<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AWS/AWS_Upload_file_to_S3_bucket.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #aws #cloud #storage #S3bucket

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

## Input

### Install packages


```python
!pip install boto3 getpass4
```

### Import library


```python
import boto3
```

### Variables


```python
ACCESS_KEY_ID = "**********"
SECRET_ACCESS_KEY = "**********"

BUCKET_NAME = "naas-example"
BUCKET_OBJECT_KEY = 'naas_happy_hour.mp3'
```

## Model

### Connect to AWS


```python
s3 = boto3.client('s3',
                  aws_access_key_id=ACCESS_KEY_ID,
                  aws_secret_access_key=SECRET_ACCESS_KEY)
```

## Output

### Upload data


```python
with open(BUCKET_OBJECT_KEY, "rb") as f:
    s3.upload_fileobj(f, BUCKET_NAME, BUCKET_OBJECT_KEY)
```
