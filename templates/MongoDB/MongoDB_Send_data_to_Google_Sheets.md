<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/MongoDB/MongoDB_Send_data_to_Google_Sheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=MongoDB+-+Send+data+to+Google+Sheets:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #mongodb #googlesheets #nosql #operations #automation

**Author:** [Oketunji Oludolapo](https://www.linkedin.com/in/oludolapo-oketunji/)

This notebook will help you send data from your MongoDB database collection to your spreadsheet

**How To Use Template:** [Video](https://drive.google.com/file/d/1lAZdZP6qk4tZepgWJtiQ6rL6D3wosPSN/view?usp=sharing)

## Input


```python
from naas_drivers import mongo, gsheet
import pandas as pd
import naas
```

### Setup MongoDB
- Get your user, password and connection URL details from your MongoDB Atlas Cluster
**How To get Required MongoDB details**: [Article](https://towardsdev.com/part-6-7-of-python-mongodb-tutorial-series-for-data-scientists-connecting-mongodb-atlas-to-python-d7169445fca1)


```python
user = "your user"
passwd = "your password"
host = "Your Connection URL"
port = 9090
collection_name = "COLLECTION NAME"
db_name = "DATABASE NAME"
```

### Setup Google Sheet
- Share your Google Sheet with our service account : 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com


```python
spreadsheet_id = "------"
sheet_name = "Sheet1"
```

### Setup Naas


```python
naas.scheduler.add(
    cron="0 9 * * *"
)  # Send in production this notebook and run it, every day at 9:00.

# use this to delete your automation
# naas.scheduler.delete()
```

## Model

### Get data in MongoDB


```python
df = mongo.connect(host, port, user, passwd).get(collection_name, db_name)
```

## Output

### Send data to Google Sheet


```python
gsheet.connect(spreadsheet_id).send(sheet_name=sheet_name, data=df, append=False)
```
