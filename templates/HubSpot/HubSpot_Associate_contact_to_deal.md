<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# HubSpot - Associate contact to deal
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Associate_contact_to_deal.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #deal #contact #naas_drivers

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

### Enter association parameters


```python
deal_id = '3452242690'
contact_id = '245201'
```

## Model

### Create association


```python
hubspot.connect(HS_API_KEY).associations.create("deal",
                                                deal_id,
                                                "contact",
                                                contact_id)
```

## Output

### Display result


```python
print("🙌 Association successfully created !")
```
