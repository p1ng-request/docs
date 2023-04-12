    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Add_image_to_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Add+image+to+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #productivity #naas_drivers #operations #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows you to easily add images to your Notion pages.

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
page.image(IMAGE_URL)
```

## Output


```python
page.update()
```
