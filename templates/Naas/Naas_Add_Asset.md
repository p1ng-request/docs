<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Add_Asset.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Add+Asset:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #asset #snipet #operations

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to copy in production a file as an asset and allow yourself to get it by calling the returned URL.

**References:**
- [Naas Documentation](https://docs.naas.ai/)
- [Naas Asset Documentation](https://docs.naas.ai/features/asset)

## Input

### Import libraries


```python
import naas
```

### Setup Variables
- `path`: path of the file to be send into production. If no path is set, the current notebook will be sent to production.
- `params`: default "{"inline": True}": Get a response in your web browser instead of downloading the result.
- `override_prod`: Boolean to be set if you want to overwritte asset link in production mode.


```python
path = None
params = {"inline": True}
override_prod = False
```

## Model

### Add Asset


```python
asset_url = naas.asset.add(path=None, override_prod=override_prod)
```

## Output

### Display result


```python
print("👌 Well done! Your Assets has been sent to production:", asset_url)
```

 
