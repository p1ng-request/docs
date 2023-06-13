<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Add_or_Update_Dependency.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Add+or+Update+Dependency:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #dependency #add #update #snippet #operation

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to add or update a dependency in Naas. The naas dependency feature push files (script, csv) into production environment. 

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Dependency Documentation](https://docs.naas.ai/features/dependency)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `path`: path of the file to be send into production. If no path is set, the current notebook will be sent to production.


```python
path = None
```

## Model

### Add or Update Dependency


```python
naas.dependency.add(path)
```

## Output

### Display result


```python
print("👌 Well done! Your Dependency has been sent to production.")
```

 
