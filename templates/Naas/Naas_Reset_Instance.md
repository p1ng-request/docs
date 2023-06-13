<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Reset_Instance.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Reset+Instance:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #scheduler #operations #snippet

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** This notebook provides a way to reset an instance of Naas, allowing users to start fresh with a clean slate.

## Input

### Load libraries


```python
import naas
```

## Model

### Reset naas instance


```python
def reset_naas_instance():
    ! rm -rf ~/.clean || true
    ! mkdir ~/.clean || true
    ! mv ~/.* ~/.clean
    naas.update()
```

## Output


```python
reset_naas_instance()
```
