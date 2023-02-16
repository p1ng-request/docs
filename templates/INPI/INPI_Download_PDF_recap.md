<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/INPI/INPI_Download_PDF_recap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=INPI+-+Download+PDF+recap:+Error+short+description">Bug report</a>

**Tags:** #inpi #pdf #snippet #url #naas #societe #opendata

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook downloads a PDF summary of INPI (Instituto Nacional da Propriedade Industrial) data.

## Input

### Import libraries


```python
import urllib
```

### Setup Variables


```python
# Input
SIREN = "8779417XX"

# Output
PDF_OUTPUT = f"RECAPITULATIF_INPI_{SIREN}.pdf"
```

## Model

### Download PDF


```python
def download_pdf(siren, filepath):
    url = f"https://data.inpi.fr/export/companies?format=pdf&ids=[%22{siren}%22]"
    response = urllib.request.urlopen(url)
    file = open(filepath, "wb")
    file.write(response.read())
    file.close()
    print("File saved:", filepath)
```

## Output

### Display result


```python
download_pdf(SIREN, PDF_OUTPUT)
```
