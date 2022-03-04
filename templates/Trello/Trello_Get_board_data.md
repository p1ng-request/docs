<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Trello - Get board data
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Trello/Trello_Get_board_data.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #trello #project #board

## Input

### Import library


```python
import trello_connector
```

## Model

### Variables


```python
token = ""
key = ""
board_id = "VCmIpC16"
export = "xls"
```

- token and key can be get from trello developer dashboard 
- board is the unique id for each trello board. it can be get from trello board url
- export can be csv or xls.

## Output

### Get board data


```python
df = trello_connector.main(key,token,board_id, export)
```
