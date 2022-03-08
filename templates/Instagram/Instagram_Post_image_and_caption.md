<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Instagram/Instagram_Post_image_and_caption.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #instagram

**Author:** [Unknown](https://www.linkedin.com/company/naas-ai/)

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
