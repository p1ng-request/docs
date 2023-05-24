<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Add_or_Update_Secret.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Add+or+Update+Secret:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #secret #add #update #operation #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel)

**Description:** This notebook will show how to add or uppdate a secret to Naas.

Secrets are an important part of Naas, when you need to interact with other services, you need secret, like any other variable the temptation is big to put it straight in your notebook, but this lead to a big security breach since we replicate a lot the notebook, in the versioning system, the output and your ability to share it or send it to git!  
Use this simple feature instead to have global secure storage share with your sandbox and production.
Secrets are local to your machine and encoded, that a big layer of security with a little effort.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Secret Documentation](https://docs.naas.ai/features/secret)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `naas_secret_name`: Name of the secret to add
- `naas_secret_value`: Value of the secret to add


```python
naas_secret_name = "YOUR_SECRET_NAME"
naas_secret_value = "YOUR_SECRET_VALUE"
```

## Model

### Add or Update Secret


```python
naas.secret.add(naas_secret_name, naas_secret_value)
```

## Output

### Return your secret store in Naas
It should get the value stored in your variable `naas_secret_value`


```python
naas.secret.get(naas_secret_name)
```

 
