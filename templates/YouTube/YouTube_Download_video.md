<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/YouTube/YouTube_Download_video.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=YouTube+-+Download+video:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #youtube #download #video #content #snippet #naas

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to download videos from YouTube.

**References:**
- [pytube library](https://pypi.org/project/pytube/)

## Input

### Import libraries


```python
try:
    from pytube import YouTube
except:
    !pip install pytube --user
    from pytube import YouTube
```

### Setup Variables
- `youtube_video_url`: YouTube video URL
- `output_dir`: Output directory to save the video.


```python
# Inputs
youtube_video_url = "https://www.youtube.com/watch?v=ONiILHFItzs"

# Outputs
output_dir = "videos"
```

## Model

### Init YouTube obj


```python
try:
    yt_obj = YouTube(youtube_video_url)
except:
    !pip install pytube --upgrade --user
    yt_obj = YouTube(youtube_video_url)
```

### Display Youtube URL streams


```python
for stream in yt_obj.streams:
    print(stream)
```

### Get MP4 Quality


```python
videos_mp4 = yt_obj.streams.filter(progressive=True, file_extension="mp4")

for videos in videos_mp4:
    print(videos)
```

### Get highest resolution


```python
video_highest_resolution = videos_mp4.get_highest_resolution()
video_highest_resolution
```

## Output

### Download video
If output_dir does not exist, it will be created


```python
video_highest_resolution.download(output_path=output_dir)
```


```python

```
