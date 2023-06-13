<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Insee/Insee_Download_PDF_recap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Insee+-+Download+PDF+recap:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #insee #pdf #snippet #url #naas #societe #opendata

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook downloads PDF summaries of data from the French National Institute of Statistics and Economic Studies (INSEE).

## Input

### Import libraries


```python
import urllib
```

### Setup Variables


```python
# Input
SIRET = "87794XXXXXXXX"

# Output
PDF_OUTPUT = f"RECAPITULATIF_INSEE_{SIRET}.pdf"
```

## Model

### Download PDF


```python
def download_pdf(siret, filepath):
    url = f"https://api.avis-situation-sirene.insee.fr/identification/pdf/{siret}"
    response = urllib.request.urlopen(url)
    file = open(filepath, "wb")
    file.write(response.read())
    file.close()
    print("File saved:", filepath)
```

## Output

### Display result


```python
download_pdf(SIRET, PDF_OUTPUT)
```
