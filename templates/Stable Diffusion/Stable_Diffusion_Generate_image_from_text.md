<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Stable%20Diffusion/Stable_Diffusion_Generate_image_from_text.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Stable+Diffusion+-+Generate+image+from+text:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #stable-diffusion #image-generation #text-to-image #ai #machine-learning #deep-learning

**Author:** [Oussama El Bahaoui](https://www.linkedin.com/in/oelbahaoui/)

**Description:** This notebook would allow you to generate image from text using Stable Diffusion. It is useful for organizations to create visuals from text for marketing purposes.

<a target="_blank" href="https://colab.research.google.com/drive/1PYhRAo8bcgSJdIFrtAFUF2ENbe5BJhn7?usp=sharing">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

**References:**
- [Stability.ai - Stable Diffusion](https://stability.ai/stable-diffusion)
- [Stability.ai - Text to Image](https://stability.ai/text-to-image)

## Note📝

This notebook requires a more powerful machine than the free tier we provide. You have two options to proceed:

1. **Using Google Colab:** If you have a Google account, you can open this notebook in Google Colab(link is above), which provides free access to more powerful computational resources to run this notebook. To do this, click the “Open in Colab” button at the top of the notebook. Please note that you may need to sign in with your Google account or create one if you don’t have it.
2. **Contacting Us for Machine Upgrade:** If you prefer to run this notebook on your own machine, you can contact us to upgrade your machine. Our team will assist you in setting up the necessary environment. Please reach out to [Jeremy Ravanel](mailto:jeremy@naas.ai) for further assistance.

Please choose the option that best suits your needs and resources.

## Input

### Install and update libraries


```python
!pip install --user --upgrade transformers diffusers accelerate
```

### Import libraries


```python
from diffusers import DiffusionPipeline, DPMSolverMultistepScheduler
from PIL import Image
import matplotlib.pyplot as plt
import torch
```

### Setup Variables


```python
## Inputs
# Model to use: this is the identifier for the model repository that we're going to use. 
# In this case, we're using the "stable-diffusion-2" model from the "stabilityai" repository.
REPO_ID = "stabilityai/stable-diffusion-2"

# This is the number of steps the model will take during inference. 
# In other words, this is the number of times the model will update its predictions.
NUM_INFERENCE_STEPS = 25

# Define the prompt: this is the description that the model will use as a basis to generate the image. 
prompt = "A person walking through a field of tall grass"

## Output
IMAGE_PATH = "output.png"
```

## Model

### Generate image from text

Using Stable Diffusion, we can generate an image from text.


```python
# Create the DiffusionPipeline
# This pipeline is created using a pretrained model from the specified repository. 
# We specify that the model should use 16-bit floating point precision for its computations 
# (which can help to save memory and improve computational speed, with a slight tradeoff in precision).
# We also specify the revision of the model to be "fp16".
pipe = DiffusionPipeline.from_pretrained(REPO_ID, torch_dtype=torch.float16, revision="fp16")

# Modify the scheduler of the pipeline
# The scheduler determines the timing of the steps in the diffusion process.
# Here, we're creating a new scheduler from the configuration of the current one, which effectively keeps the current scheduler's settings.
pipe.scheduler = DPMSolverMultistepScheduler.from_config(pipe.scheduler.config)

# Move the pipeline to GPU
# This moves all the computations of the pipeline to the GPU, which is typically much faster than the CPU for these types of tasks.
pipe = pipe.to("cuda")
```

## Output

### Generate the image


```python
# Generate an image from a prompt
# This line uses the diffusion pipeline to generate an image from the provided prompt.
# The number of inference steps specified is used in the generation process.
# The output of the pipeline is a batch of images, and we're taking the first one from this batch.
image = pipe(prompt, num_inference_steps=NUM_INFERENCE_STEPS).images[0]
```

### Save and display the image


```python
# Save the image
image.save(IMAGE_PATH)

# Display the image using matplotlib
img = Image.open(IMAGE_PATH)
plt.imshow(img)
plt.show()
```
