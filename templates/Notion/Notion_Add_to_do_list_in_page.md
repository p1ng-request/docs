<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Add_to_do_list_in_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Add+to+do+list+in+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #todo #page #snippet #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to add a to do list in a Notion page using naas_drivers from a list.

**References:**
- [Notion Drivers](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/notion.py)

## Input

### Import libraries


```python
from naas_drivers import notion
import naas
```

### Setup Variables
[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `to_do_name`: Name of your to do list
- `to_do_list`: List of actions to do
- `notion_token`: Notion token shared with your database
- `page_url`: Notion page URL or ID


```python
# Inputs
to_do_name = "My first todo:"
to_do_list = [
    "Task1",
    "Task2",
    "Task3",
]

# Outputs
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
page_url = "https://www.notion.so/naas-official/Test-93655d0408c14923bcd305dd4599cda9?pvs=4"
```

## Model

### Add to do list


```python
page_id = page_url.split("/")[-1].split("?")[0].split("-")[-1]
page = notion.connect(notion_token).page.get(page_id)
page.paragraph(to_do_name)
for to_do in to_do_list: 
    page.to_do(to_do)
page.update()
```

## Output

### Display result


```python
print("To do list updated in your page:", page_url)
```

 
