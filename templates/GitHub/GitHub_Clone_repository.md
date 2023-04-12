    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Clone_repository.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Clone+repository:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #snippet #operations #repository

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook clones a GitHub repository to your naas.

## Input

### Import libraries


```python
from IPython.display import display
from ipywidgets import widgets
import naas
from os import path
```

### Define your repository URL


```python
GIT_REPO_URL = "https://github.com/jupyter-naas/data-product-framework.git"
```

## Model

### Setup project path and clone repo


```python
# Setup folder path
PROJECT_NAME = GIT_REPO_URL.split("/")[-1].replace(".git", "")
GIT_REPO_PATH = path.join("/", "home", "ftp", PROJECT_NAME)

# Download repo inside folder
!git clone "$GIT_REPO_URL" "$GIT_REPO_PATH"
```

## Output

#### Display result


```python
print(f"✅ The project has been downloaded to the following folder: {GIT_REPO_PATH}.")
```
