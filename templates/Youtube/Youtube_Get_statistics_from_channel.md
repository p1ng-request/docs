<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Youtube - Get statistics from channel
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Youtube/Youtube_Get_statistics_from_channel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #youtube #channel #statistics #naas_drivers

## Input

### Import library


```python
import naas
from naas_drivers import youtube
```

### Variables


```python
# Youtube api Key
YOUTUBE_API_KEY = naas.secret.get('YOUTUBE_API_KEY')

# Channel ID
channel_url = "https://www.youtube.com/channel/UCKKG5hzjXXU_rRdHHWQ8JHQ"
```

## Model


```python
df_stats = youtube.connect(YOUTUBE_API_KEY).channel.get_statistics(channel_url)
```

## Output

### Display results


```python
df_stats
```
