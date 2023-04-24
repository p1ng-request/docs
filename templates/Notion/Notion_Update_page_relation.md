<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Update_page_relation.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Update+page+relation:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #update #page #relation #requests #api

**Author:** [Florent Ravenel](https://linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to update page relation using requests. It is usefull for organization to link different database in Notion and keep track of their data.

**References:**
- [Notion API Reference](https://developers.notion.com/reference/page-property-values#relation)

## Input

### Import libraries


```python
import requests
import naas
from pprint import pprint
```

### Setup Variables
[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `notion_token`: Notion token shared with your database
- `page_id`: Notion page URL or ID
- `relation_property_name`: Relation property name in your page
- `relation_id`: Page URL or ID to be linked to master page as relation


```python
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
page_id = "https://www.notion.so/asgard-group/EUROPA-VELIZY-41a024aa918347648d63f531736ca141?pvs=4"
relation_property_name = "<relation_property_name>"
relation_id = "https://www.notion.so/asgard-group/LOKACOM-LEVALLOIS-PERRET-b2f91c6a5d32404997bb0232713400d7?pvs=4"
```

## Model

### Get page


```python
# Get page ID
page_id = page_id.split("?")[0].split("-")[-1]

# Get properties from page
url = f"https://api.notion.com/v1/pages/{page_id}"
headers = {
    'Authorization': f'Bearer {notion_token}',
    "accept": "application/json",
    "Notion-Version": "2022-06-28"
}
response = requests.get(url, headers=headers)
properties = response.json().get("properties")
pprint(properties)
```

## Output

### Update page relation


```python
# Get relation ID
relation_id = relation_id.split("?")[0].split("-")[-1]

# Update properties from page
properties[relation_property_name]["relation"] = [{'id': relation_id}]
res = requests.patch(url, headers=headers, json={"properties": properties})
if res.status_code == 200:
    print("Relation updated for page:", page_id)
```
