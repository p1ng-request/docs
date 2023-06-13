<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Add_cover_image_to_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Add+cover+image+to+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #productivity #naas_drivers #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** This notebook allows you to add a cover image to a page in Notion.

## Input

### Import libraries


```python
from naas_drivers import notion
```

### Setup Notion
- [Get your Notion integration token](https://docs.naas.ai/drivers/notion)
- Share integration with your database / page


```python
# Enter Token API
NOTION_TOKEN = "ENTER_YOUR_NOTION_TOKEN_HERE"  # EXAMPLE: "secret_xxxxxxxxxxxxxxxxxx"

# Enter Page URL
PAGE_URL = "ENTER_YOUR_PAGE_URL_HERE"  # EXAMPLE: "https://www.notion.so/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Enter icon URL
IMAGE_URL = "ENTER_YOUR_IMAGE_URL_HERE"  # EXAMPLE: "https://XXXXXXXXXXXX.png"
```

## Model

### Get page


```python
page = notion.connect(NOTION_TOKEN).page.get(PAGE_URL)
```

### Add icon image to page


```python
notion.client.pages.update(
    page_id=page.id, cover={"type": "external", "external": {"url": IMAGE_URL}}
)
```

## Output


```python
page.update()
```
