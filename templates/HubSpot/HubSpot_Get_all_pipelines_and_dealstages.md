<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_all_pipelines_and_dealstages.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=HubSpot+-+Get+all+pipelines+and+dealstages:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #hubspot #crm #sales #deal #pipelines #naas_drivers #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook get all your pipelines and dealstages.

## Input

### Import libraries


```python
from naas_drivers import hubspot
import naas
```

### Setup HubSpot
[Get your HubSpot Access token](https://knowledge.hubspot.com/articles/kcs_article/integrations/how-do-i-get-my-hubspot-api-key)
- `hs_access_token`: This variable stores an access token used for accessing the HubSpot API. It is retrieved from a secret store using naas.secret.get() method. If the access token is not available in the secret store, a default value of "YOUR_HS_ACCESS_TOKEN" is used.


```python
hs_access_token = naas.secret.get("HS_ACCESS_TOKEN") or "YOUR_HS_ACCESS_TOKEN"
```

## Model

### Get pipelines and dealstages


```python
df_pipelines = hubspot.connect(hs_access_token).pipelines.get_all()
```

## Output

### Display result


```python
df_pipelines
```
