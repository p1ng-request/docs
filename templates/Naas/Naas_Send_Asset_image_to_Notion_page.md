<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Send_Asset_image_to_Notion_page.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Send+Asset+image+to+Notion+page:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #notion #image #asset #send #vizualise

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook sends an naas image asset to a Notion page. It could be usefull to push chart created in plotly to Notion. If your page is in a notion database, you will be able to vizualise the chart in Gallery (display page content). The image asset will be updated (deleted and added) to make sure the graph display is always up to date in Notion.

**References:**
- [Naas Documentation](https://docs.naas.io/)
- [Notion Documentation](https://www.notion.so/product/Notion-cffd2f2fad6e4f9fae9c563d9f0e4e53)

## Input

### Import libraries


```python
from naas_drivers import notion
import plotly.graph_objects as go
import naas
```

### Setup Variables
[Create integration with Notion](https://developers.notion.com/docs/create-a-notion-integration)
- `output_image`: Image output path
- `notion_token`: Notion token shared with your database
- `page_url`: Notion page URL or ID


```python
output_image = "image.png"
notion_token = naas.secret.get("NOTION_TOKEN") or "YOUR_TOKEN"
page_url = "https://www.notion.so/naas-official/Test-f01437dd2b414edfbfe7a45c36966b13?pvs=4"
```

## Model

### Create Waterfall chart


```python
title = "EBITDA (simple)"
fig = go.Figure(
    go.Waterfall(
        name="20",
        orientation="v",
        measure=["relative", "relative", "total", "relative", "relative", "total"],
        decreasing={"marker": {"color": "#d94228"}},
        increasing={"marker": {"color": "#5ee290"}},
        totals={"marker": {"color": "#3f3f3f"}},
        x=[
            "Sales",
            "Consulting",
            "Revenue",
            "Direct expenses",
            "Other expenses",
            "EBITDA",
        ],
        textposition="outside",
        text=["+60", "+80", "140", "-40", "-20", "80"],
        y=[60, 80, 0, -40, -20, 0],
        connector={"line": {"color": "white"}},
    )
)

fig.update_layout(
    title=title,
    plot_bgcolor="#ffffff",
    width=800,
    height=600,
    xaxis_tickfont_size=14,
    yaxis=dict(
        title="USD (millions)",
        titlefont_size=16,
        tickfont_size=14,
    ),
    legend=dict(x=0, y=1.0, bgcolor="white", bordercolor="white"),
    bargap=0.1,  # gap between bars of adjacent location coordinates.
    bargroupgap=0.1,  # gap between bars of the same location coordinate.
)
config = {"displayModeBar": False}
fig.show(config=config)
```

### Export in PNG and HTML


```python
fig.write_image(output_image)
```

### Add naas asset


```python
asset_link = naas.asset.add(output_image)
```

### Upload image


```python
page_id = page_url.split("/")[-1].split("?")[0].split("-")[-1]
page = notion.connect(notion_token).page.get(page_id)

# Check if image already exists
blocks = page.get_blocks()
for block in blocks:
    content_block = getattr(block, block.type)
    if block.type == "image":
        image_url = block.image.external.url
        if image_url.startswith("https://public.naas.ai/"):
            notion.connect(notion_token).blocks.delete(block.id)
            
page.image(asset_link)
page.update()
```

## Output

### Display result


```python
print("Image uploaded in your page:", page_url)
```

 

 
