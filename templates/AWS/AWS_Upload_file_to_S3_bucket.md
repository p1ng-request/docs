<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/AWS/AWS_Upload_file_to_S3_bucket.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=AWS+-+Upload+file+to+S3+bucket:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #aws #cloud #storage #S3bucket #snippet #operations# AWS - Upload file to S3 bucket

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou/)

**Description:** This notebook provides instructions on how to upload a file to an Amazon Web Services (AWS) S3 bucket, allowing for secure storage and easy access to the file. It is a simple and efficient way to store and manage data in the cloud.

## Input

### Import library


```python
try:
    import boto3
except:
    !pip install boto3 getpass4
    import boto3
```

### Variables


```python
ACCESS_KEY_ID = "**********"
SECRET_ACCESS_KEY = "**********"

BUCKET_NAME = "naas-example"
BUCKET_OBJECT_KEY = "naas_happy_hour.mp3"
```

## Model

### Connect to AWS


```python
s3 = boto3.client(
    "s3", aws_access_key_id=ACCESS_KEY_ID, aws_secret_access_key=SECRET_ACCESS_KEY
)
```

## Output

### Upload data


```python
with open(BUCKET_OBJECT_KEY, "rb") as f:
    s3.upload_fileobj(f, BUCKET_NAME, BUCKET_OBJECT_KEY)
```
