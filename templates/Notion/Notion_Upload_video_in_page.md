<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Notion/Notion_Upload_video_in_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Notion+-+Upload+video+in+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #notion #upload #video #page #snippet #naas_drivers

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook explains how to upload a video in a Notion page using naas_drivers. It is usefull for organizations that need to add videos to their Notion pages.

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
- `video_url`: Video URL
- `notion_token`: Notion token shared with your database
- `page_url`: Notion page URL or ID


```python
# Inputs
video_url = "https://www.youtube.com/watch?v=ONiILHFItzs"

# Outputs
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
page_url = "https://www.notion.so/naas-official/Test-93655d0408c14923bcd305dd4599cda9?pvs=4"
```

## Model

### Upload video


```python
page_id = page_url.split("/")[-1].split("?")[0].split("-")[-1]
page = notion.connect(notion_token).page.get(page_id)
page.video(video_url)
page.update()
```

## Output

### Display result


```python
print("Video uploaded in your page:", page_url)
```

 
