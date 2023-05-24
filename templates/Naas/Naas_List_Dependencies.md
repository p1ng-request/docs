<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_List_Dependencies.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+List+Dependencies:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #dependency #snipet #operations #list

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to list current dependencies in production.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Dependency Documentation](https://docs.naas.ai/features/dependency)

## Input

### Import libraries


```python
import naas
```

## Model

### List current Dependencies


```python
dependencies = naas.dependency.currents()
```

## Output

### Display result


```python
print("Dependencies found in production:", len(dependencies))
dependencies.head(5)
```

 
