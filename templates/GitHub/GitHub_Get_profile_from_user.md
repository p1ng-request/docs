    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Get_profile_from_user.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Get+profile+from+user:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #user #profile #operations #snippet #dataframe

**Author:** [Sanjeet Attili](https://www.linkedin.com/in/sanjeet-attili-760bab190/)

**Description:** This notebook provides a way to retrieve a user's profile information from GitHub.

## Input

### Imports


```python
from naas_drivers import github
```

### Variables


```python
USER_URL = "https://github.com/FlorentLvr"

GITHUB_TOKEN = "ghp_Stz3qlkR3b00nKUW8rxJoxxxxxxxxxxxx"
```

## Model

### Get profile from user


```python
df_user = github.connect(GITHUB_TOKEN).users.get_profile(USER_URL)
```

## Output

### Display result


```python
df_user
```
