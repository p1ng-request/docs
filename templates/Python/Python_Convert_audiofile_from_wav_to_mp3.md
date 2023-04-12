<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Convert_audiofile_from_wav_to_mp3.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Convert+audiofile+from+wav+to+mp3:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #audio #wavtomp3 #pydub

**Author:** Mohit Singh

**Description:** This notebook uses the Pydub library to convert audio file from wav to mp3.

## Input

### Download ffmpeg


```python
!wget "https://johnvansickle.com/ffmpeg/builds/ffmpeg-git-amd64-static.tar.xz"
!tar xf ffmpeg-git-amd64-static.tar.xz
!mv ffmpeg-git-20230313-amd64-static ffmpeg
```


```python
import os
new_path = os.path.join(os.getcwd(), "ffmpeg")
%env PATH=$new_path
```

### Import libraries


```python
try:
    from pydub import AudioSegment
except:
    !pip install pydub
    from pydub import AudioSegment
import requests
```

### Setup Variables
- `audio_file_url`: Link of audio file in wav to be converted to mp3


```python
# Inputs
## link of sample wav file
audio_file_url = 'https://file-examples.com/storage/fef1706276640fa2f99a5a4/2017/11/file_example_WAV_1MG.wav'
wav_path = 'audio.wav'

##Output
mp3_path = 'audio.mp3'
```

## Model

### Get and save audio file from URL


```python
response = requests.get(audio_file_url)
open("audio.wav", "wb").write(response.content)
```

### Convert wav to mp3
This code will convert the audio file from wav to mp3.


```python
# read the WAV file using pydub
wav_audio = AudioSegment.from_file("audio.wav", format="wav")

# export the audio as MP3 using pydub
wav_audio.export(mp3_path, format="mp3")
```

## Output

### Display result
This code will check if audio file is successfully converted to mp3.


```python
if (os.path.isfile(mp3_path)):
    print('Conversion of audio file from wav to mp3 is successful')
```
