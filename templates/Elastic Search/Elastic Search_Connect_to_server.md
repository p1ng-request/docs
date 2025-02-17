# Connect to server

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/open\_in\_naas.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Elastic%20Search/Elastic%20Search\_Connect\_to\_server.ipynb)

**Tags:** #elastic #search #snippet

**Author:** [Ebin Paulose](https://www.linkedin.com/in/ebinpaulose/)

#### 1. Prerequisites

* python3
* ubuntu 18.04
* java1.8

#### 2. Elasticsearch on local machine

**Install Linux packages**

```
$ sudo apt update
$ sudo apt-get install apt-transport-http
$ wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
$ sudo add-apt-repository "deb https://artifacts.elastic.co/packages/7.x/apt stable main"
$ sudo apt update
$ sudo apt install elasticsearch 
```

**Check status of Elasticsearch server (Local)**

```
$ sudo /etc/init.d/elasticsearch status
```

**Start Elasticsearch server (Local)**

```
$ sudo /etc/init.d/elasticsearch start
```

**Note : Install Java 1.8 and set Java environment variables path**

#### 3. Elasticsearch on cloud

**Step 1: Login to https://www.elastic.co/ and create a deployment**

**Step 2: On successful deployment get credentials**

**Step 3: Create Elasticsearch credentials JSON**

**Credentials Json format**

```
{
	"endpoint": "< Elasticsearch endpoint from elasticsearch cloud >",
	"port": "< Port number as mentioned in elasticsearch cloud >",
	"user": "< User as mentioned in elasticsearch cloud >",
	"password": "< Elasticsearch cloud user password >",
	"protocol": "https"
}
```

#### 4. Python connector for Elasticsearch

### Input

#### Import library

```python
from elasticsearchconnector import ElasticsearchConnector
```

### Model

```python
instance = ElasticsearchConnector("sample_credentials.json")
```

#### Send data to Elasticsearch server

```python
# parameters = {'index':'< Name of the index >','type':' < Document name > '}
parameters = {'index':'students','type':'engineering'}
# data = { < Key value pairs > }
data = {"Name": "Poul", "Age":20, "address": "New york"}
result = instance.save_data(parameters,data)
```

#### Search data from Elasticsearch server

```python
# parameters = {'index':'< Name of the index >','type':' < Document name > '}
parameters = {'index':'students','type':'engineering'}
```

### Output

#### Single search

```python
# Single search
q1 = {"query": {"match": {'Name':'Poul'}}}
result = instance.search_data(parameters,[q1],search_type='search')
print(result)
```

#### Multiple search

```python
# Multiple search
q1 = {"query": {"match": {'Name':'Poul'}}}
q2 = {"query": {"match": {'Age':27}}}
result = instance.search_data(parameters,[q1,q2],search_type='msearch')
print(result)
```
