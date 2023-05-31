<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WhatsApp/WhatsApp_Create_heatmap_of_activities.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WhatsApp+-+Create+heatmap+of+activities:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #whatsapp #naas_drivers #naas #visualisation #chatminers #heatmap

**Author:** [Hamid Mukhtar](https://www.linkedin.com/in/mukhtar-hamid/)

**Description:** This notebook creates a heatmap of your chat activities.

## Input

### Import libraries


```python
try:
    import chatminer
except:
    !pip install chat-miner --user
from chatminer.chatparsers import WhatsAppParser
import chatminer.visualizations as vis
import matplotlib.pyplot as plt
```

### Setup Variables

**Export chat history**

You can use the export chat feature to export a copy of the chat history from an individual or group chat.
1. Open the individual or group chat.
2. Tap > More > Export chat.
3. Choose to export without media.
4. Save it to your drive or choose your preferred option.

- `file_path`: file path of your chat in txt


```python
file_path = "Chat WhatsApp with +00 0 00 00 00 00.txt"
```

## Model

### Open & Parse chat file


```python
parser = WhatsAppParser(file_path)
parser.parse_file()
df = parser.parsed_messages.get_df()
df.head()
```

## Output

### Create heatmap


```python
fig, ax = plt.subplots(2, 1, figsize=(20, 10))
ax[0] = vis.calendar_heatmap(df, year=2023, cmap='Oranges', ax=ax[0])
ax[1] = vis.calendar_heatmap(df, year=2023, linewidth=0, monthly_border=True, ax=ax[1])
```
