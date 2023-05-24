<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Delete_Dependency.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Delete+Dependency:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #dependency #snipet #operations #delete

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to delete a dependency from naas production environment.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Dependency Documentation](https://docs.naas.ai/features/dependency)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `path`: Go to your Naas manager, section "Jobs" and copy/paste the path of the dependency you want to delete.

If this notebook is not on your root folder, you need to set absolute path of your notebook starting with "/home/ftp/".   


```python
path = "/home/ftp/"
```

## Model

### Delete Asset


```python
naas.dependency.delete(path=path)
```

## Output

### Display result


```python
print("🗑 Done! Your Dependency has been remove from production.")
```

 
