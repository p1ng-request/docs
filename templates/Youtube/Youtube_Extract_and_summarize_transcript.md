<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Youtube/Youtube_Extract_and_summarize_transcript.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

The objective is to summarize the transcript from Youtube with Hugging Face Naas drivers using T5small model.

**Tags:** #youtube #transcript #video #summarize

## Input

### Install packages


```python
!pip install youtube_transcript_api
```

### Import library


```python
from youtube_transcript_api import YouTubeTranscriptApi
from naas_drivers import huggingface
```

### Variables


```python
video_id = "I6XbLIRa0v0"
file_name = "What on earth is data science?"
```

## Model

### Extract the transcript in JSON


```python
json = YouTubeTranscriptApi.get_transcript(video_id)
```

### Parse JSON in text string


```python
para = ""
for i in json :
    para += i["text"]
    para += " "
para
```


```python
text = huggingface.get("summarization", model="t5-small", tokenizer="t5-small")(para)
```

## Output

### Display results


```python
text
```
