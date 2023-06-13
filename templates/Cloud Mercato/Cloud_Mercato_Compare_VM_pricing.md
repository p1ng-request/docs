<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Cloud%20Mercato/Cloud_Mercato_Compare_VM_pricing.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Cloud+Mercato+-+Compare+VM+pricing:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #cloud #infrastruture #pricing #vm #iaas #analytics #compute

**Author:** [Anthony Monthe](https://www.linkedin.com/in/anthonymonthe/)

**Description:** Cloud Mercato is an online platform that allows users to compare virtual machine pricing from different cloud providers.

## Input

### Import libraries


```python
import requests
import pandas as pd
import naas
```

### Setup Variables

- [Create your token](graphql.cloud-mercato.com)
- You can access data without a token but you are limited to 3 requests/days
- Get a paid account to have access to VM with +16 CPUs


```python
# Input
CPU = 4  #  in CPU number
RAM = 2  # in GB
# Anonymous users are limited
TOKEN = None

# Output
csv_output = "cloud-mercato-vm-pricing.csv"
```

## Model

### Declare constants


```python
COLUMN_PARAMS = {
    "table-col-provider": "on",
    "table-col-name": "on",
    "table-col-cpu_number": "on",
    "table-col-ram": "on",
    "table-col-hourly": "on",
    "table-col-monthly": "on",
    "table-col-yearly1_noupfront": "on",
    "table-col-yearly1_parupfront": "on",
    "table-col-yearly1_parupfront_fee": "on",
    "table-col-yearly1_allupfront_fee": "on",
    "table-col-yearly2_noupfront": "on",
    "table-col-yearly2_parupfront": "on",
    "table-col-yearly2_parupfront_fee": "on",
    "table-col-yearly2_allupfront_fee": "on",
    "table-col-yearly3_noupfront": "on",
    "table-col-yearly3_parupfront": "on",
    "table-col-yearly3_parupfront_fee": "on",
    "table-col-yearly3_allupfront_fee": "on",
    "table-col-currency": "on",
    "table-col-rate": "on",
}
```


```python
FILTER_PARAMS = {
    "cpu_number_min": CPU,
    "cpu_number_max": CPU,
    "ram_min": RAM - 1,
    "ram_max": RAM + 1,
    "currency-currency": "USD",
}
```

### Get data using request


```python
params = {}
params.update(COLUMN_PARAMS)
params.update(FILTER_PARAMS)

headers = {}
if TOKEN:
    headers["Authorization"] = "Token %s" % TOKEN

response = requests.get(
    "https://p2p.cloud-mercato.com/flavors/csv",
    params=params,
    headers=headers,
    stream=True,
)
if response.status_code == 429:
    raise Exception("Download is limited for free users. Please wait or subscribe.")

df = pd.read_csv(response.raw)

print("Shape: ", df.shape)
df
```

## Output

### Save result in csv


```python
df.to_csv(csv_output, index=False)
```

### Share csv output with naas


```python
naas.asset.add(csv_output)

# -> Uncomment the line below to remove your asset
# naas.asset.delete()
```
