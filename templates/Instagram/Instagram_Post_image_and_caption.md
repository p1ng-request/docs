<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Instagram - Post image and caption
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Instagram/Instagram_Post_image_and_caption.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #instagram

## Input

### Install packages


```python
pip install instabot --user
```

### Import library


```python
from instabot import Bot 
import naas
```

## Model

### Connect to your instagram account


```python
bot = Bot() 
bot.login(username = "USERNAME",  
          password = "PASSWORD") 
```

## Output

### Upload photo


```python
bot.upload_photo("demo.jpg",
                 caption ="Naas is doing this.") 
```
