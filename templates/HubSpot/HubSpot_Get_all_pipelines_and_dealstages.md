<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_all_pipelines_and_dealstages.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #deal #pipelines #naas_drivers #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input

### Import library


```python
from naas_drivers import hubspot
```

### Setup your HubSpot
👉 Access your [HubSpot API key](https://knowledge.hubspot.com/integrations/how-do-i-get-my-hubspot-api-key)


```python
HS_API_KEY = 'YOUR_HUBSPOT_API_KEY'
```

## Model

### Get pipelines and dealstages


```python
df_pipelines = hubspot.connect(HS_API_KEY).pipelines.get_all()
```

## Output

### Display result


```python
df_pipelines
```
