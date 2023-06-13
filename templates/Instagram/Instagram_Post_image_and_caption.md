<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Instagram/Instagram_Post_image_and_caption.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Instagram+-+Post+image+and+caption:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #instagram #snippet #content

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to post images and captions to their Instagram account.

## Input

### Import libraries


```python
try:
    from instabot import Bot
except:
    pip install instabot --user
    from instabot import Bot
import naas
```

### Setup your Instagram


```python
# Credentials
username = "USERNAME"
password = "PASSWORD"

# Instragram outputs
image_path = "demo.jpg"
caption = "Naas is doing this."
```

## Model

### Connect to your instagram account


```python
bot = Bot()
bot.login(username=username, password=password)
```

## Output

### Upload photo


```python
bot.upload_photo(image_path, caption=caption)
```
