<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Qonto/Qonto_Get_positions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Qonto+-+Get+positions:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #qonto #bank #organizations #positions #naas_drivers #finance #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides an overview of the positions available through Qonto, a digital banking service.

## Input

### Import library


```python
from naas_drivers import qonto
```

### Get your Qonto credentials
<a href='https://www.notion.so/naas-official/Qonto-driver-Get-your-credentials-0cc97828b4e7467c8bfbcf704a77e5f4'>How to get your credentials ?</a>


```python
QONTO_USER_ID = "YOUR_USER_ID"
QONTO_SECRET_KEY = "YOUR_SECRET_KEY"
```

## Model

### Get bank positions


```python
df_positions = qonto.connect(QONTO_USER_ID, QONTO_SECRET_KEY).positions.get()
```

## Output

### Display result


```python
df_positions
```
