<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Insee/Insee_Download_PDF_recap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #insee #pdf #snippet #url #naas #societe #opendata

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

Ce document récupère les informations établies d'une société au REGISTRE NATIONAL DU COMMERCE ET DES SOCIÉTÉS :
- Description de l'entreprise
- Description de l'établissement

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
    file = open(filepath, 'wb')
    file.write(response.read())
    file.close()
    print("File saved:", filepath) 
```

## Output

### Display result


```python
download_pdf(SIRET, PDF_OUTPUT)
```
