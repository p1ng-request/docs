    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/gTTS/gTTS_Save_Text_to_Speech_to_MP3.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=gTTS+-+Save+Text+to+Speech+to+MP3:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #gTTS #texttospeech #mp3 #python #library #audio

**Author:** [Sriniketh Jayasendil](http://linkedin.com/in/sriniketh-jayasendil/)

**Description:** This notebook will demonstrate how to use the gTTS library to save text to speech as an MP3 file.

**References:**
- [gTTS Documentation](https://pypi.org/project/gTTS/)
- [gTTS GitHub Repository](https://github.com/pndurette/gTTS)

## Input

### Import libraries


```python
try:
    from gtts import gTTS

except ModuleNotFoundError:
    !pip install gTTS
    from gtts import gTTS
```

### Setup Variables
- `text`: Text to be converted to speech


```python
text = "This is a demonstration of the gTTS library"
```

## Model

### Convert Text to Speech

This code will convert the text to speech and save it as an MP3 file.


```python
tts = gTTS(text=text, lang="en")
tts.save("text_to_speech.mp3")
```

## Output

### Display result

This code will display the result of the conversion.


```python
print("Text to Speech conversion successful!")
```

 
