<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_image_from_text.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+image+from+text:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #image #text #generation

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/jeremyravenel)

**Description:** This notebook shows how to use the OpenAI API to make create images from text using Dall-E.

**References:**
- [Dall-E](https://openai.com/research/dall-e)

## Input

### Install package


```python
import os
try:
    import openai # OpenAI Python library to make API calls
    import requests  # used to download images
    import os  # used to access filepaths
    from PIL import Image  # used to print and edit images
    import naas  # used to generate shareable image link
except ModuleNotFoundError:
    !pip install --user openai
    import openai
```

### Setup Variables
- `api_key`: OpenAI API key. [Get your API key here](https://openai.com/docs/api-overview/).
- `n` (int): The number of images to generate. Must be between 1 and 10. Defaults to 1.
- `size` (str): The size of the generated images. Must be one of "256x256", "512x512", or "1024x1024". Smaller images are faster. Defaults to "1024x1024".
- `response_format` (str): The format in which the generated images are returned. Must be one of "url" or "b64_json". Defaults to "url".
- `user` (str): A unique identifier representing your end-user, which will help OpenAI to monitor and detect abuse. [Learn more.](https://beta.openai.com/docs/usage-policies/end-user-ids)


```python
api_key = naas.secret.get("OPENAI_API_KEY")
prompt = "A dragon spreading fire on a house, realistic art"
n = 1
size = "1024x1024"
response_format = "url"
```

## Model

### Generate image


```python
openai.api_key = api_key

# call the OpenAI API
generation_response = openai.Image.create(
    prompt=prompt,
    n=n,
    size=size,
    response_format=response_format,
)

# print response
print(generation_response)
```

### Save image


```python
# set a directory to save DALL-E images to
image_dir_name = "images"
image_dir = os.path.join(os.curdir, image_dir_name)

# create the directory if it doesn't yet exist
if not os.path.isdir(image_dir):
    os.mkdir(image_dir)

# print the directory to save to
print(f"{image_dir=}")

# save the image
generated_image_name = "generated_image.png"  # any name you like; the filetype should be .png
generated_image_filepath = os.path.join(image_dir, generated_image_name)
generated_image_url = generation_response["data"][0]["url"]  # extract image URL from response
generated_image = requests.get(generated_image_url).content  # download the image

with open(generated_image_filepath, "wb") as image_file:
    image_file.write(generated_image)  # write the image to the file
```

## Output

### Show Image


```python
# print the image
print(generated_image_filepath)
display(Image.open(generated_image_filepath))
```

### Create shareable asset 


```python
naas.asset.add(generated_image_filepath)
```
