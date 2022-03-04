<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Notion - Push data from Gsheets
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Push_data_from_Gsheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

## Input

### Import librairies


```python
from naas_drivers import notion, gsheet
import pandas as pd
```

### Variables


```python
# Notion
token = ""
database_id = ""

# Gsheet
spreadsheet_id = "SPREADSHEET_ID"
sheet_name = 'NAME_OF_THE_SHEET'
```

### Mapping the columns name


```python
mapping = {
    "NAME_OF_THE_COLUMN_IN_THE_SHEET": 'NAME_OF_THE_COLUMN_IN_NOTION'
}
```

### Get database from notion


```python
database = notion.connect(token).database.get(database_id)
df_db = database.df()
df_db
```

### Get unique Token from notion database


```python
# The unique Token is a variable that serve to compare the two set of data
try:
    tokens = df_db.Token.unique()
    tokens
except:
    tokens = []
```

### Get data from gsheet


```python
df_gsheets = gsheet.connect(spreadsheet_id).get(sheet_name)
df_gsheets
```

## Model

### Cleaning gsheet


```python
gs_clean = df_gsheets.copy()

# Change columns name to match with notion database
gs_clean = gs_clean.rename(columns=mapping)

gs_clean
```

### Concat dataframe and rows to update


```python
df_concat = pd.concat([gs_clean, df_db]).drop_duplicates(keep=False).drop_duplicates("Token", keep='first').reset_index(drop=True)
df_concat
```

## Output

### Update page in notion


```python
def update_page_in_notion(page, df_gsheets):
    responses = df_gsheets.values
    for response in responses:
        # response[14] is the token receive from the sheets data
        if response[14] == token:
            # Here you can map the page of the DB with your data from the sheet
            page.title("Token", response[14])
    page.update()
```

### Write page in notion


```python
def write_in_notion(df_gsheets, database, token):
    responses = df_gsheets.values
    page = notion.Page.new(database_id=database_id).create()
    for response in responses:
        # response[14] is the token receive from the sheets data
        if response[14] == token:
            # Here you can map the page of the DB with your data from the sheet
            page.title("Token", response[14])
    page.update()
```

### Sync Gsheet with Notion database


```python
for _, row in df_concat.iterrows():
    print(_)
    token = row.Token
    if token in tokens:
        # Update dabase in notion
        print("Update database :", token)
        for page in database.query():
            page_temp = page.df()
            if token == page_temp.values[9][2]:
                print("Updating..")
                update_page_in_notion(page, df_concat, token)
    else:
        # Create page in notion database
        print("New page created in Notion :")
        write_in_notion(df_concat, database, token)
```
