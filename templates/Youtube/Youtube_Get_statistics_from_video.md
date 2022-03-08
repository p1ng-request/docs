<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Youtube/Youtube_Get_statistics_from_video.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #youtube #video #statistics #naas_drivers

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
video_url = "https://www.youtube.com/watch?v=W8H57kam9kg&t=3685s"
```

## Model


```python
df_stats = youtube.connect(YOUTUBE_API_KEY).video.get_statistics(video_url)
```

## Output

### Display results


```python
df_stats
```
