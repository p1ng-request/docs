<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Add_heading_in_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Add+heading+in+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #heading #page #organization #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook explains how to add headings in a Notion page using naas_drivers.

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
- `heading_1`: Heading 1 text to be added in Notion
- `heading_2`: Heading 2 text to be added in Notion
- `heading_3`: Heading 3 text to be added in Notion
- `paragraph`: Pagraph text to be added in Notion
- `notion_token`: Notion token shared with your database
- `page_url`: Notion page URL or ID


```python
# Inputs
heading_1 = "Naas - Notion"
heading_2 = "Tips & tricks"
heading_3 = "How to add headings?"
paragraph = "To add headings, just use naas_drivers and this template."

# Outputs
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
page_url = "https://www.notion.so/naas-official/Test-93655d0408c14923bcd305dd4599cda9?pvs=4"
```

## Model

### Add code block in page


```python
page_id = page_url.split("/")[-1].split("?")[0].split("-")[-1]
page = notion.connect(notion_token).page.get(page_id)
page.heading_1(heading_1)
page.heading_2(heading_2)
page.heading_3(heading_3)
page.paragraph(paragraph)
page.update()
```

## Output

### Display result


```python
print("Headings added in your page:", page_url)
```
