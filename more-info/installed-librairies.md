---
description: List of lib installed in your naas machine (cloud only)
---

# 💃 Installed librairies

If you need to install a new lib do : 

```text
!pip install --user YOURLIB
```

You can also request to have it installed globally in our canny

{% embed url="https://naas.canny.io/" %}



{% hint style="info" %}
All libraries listed below are essential to Naas, please don't update them!
{% endhint %}

## Python level

```text
# install by naas

"nbconvert==6.0.7",
"nest_asyncio==1.5.1",
"ipywidgets==7.6.3",
"papermill==2.3.3",
"pretty-cron==1.2.0",
"APScheduler==3.7.0",
"pycron==3.0.0",
"aiohttp==3.7.4",
"html5lib==1.1",
"Pillow==8.1.2",
"markdown2==2.4.0",
"pandas==1.2.3",
"escapism==1.0.1",
"notebook==6.2.0",
"ipython==7.21.0",
"ipykernel==5.5.0",
"requests==2.25.1",
"sentry-sdk==1.0.0",
"sanic==20.12.2",
"sanic-openapi==0.6.2",
"argparse==1.4.0",
"nbclient==0.5.3",
"beautifulsoup4==4.9.3",
"tzdata"

# install by naas_drivers

"imap_tools==0.38.1",
"slackclient==2.9.3",
"pymsteams==0.1.14",
"pdfkit==0.6.1",
"markdown2==2.4.0",
"newsapi-python==0.2.6",
"airtable-python-wrapper==0.15.1",
"notion==0.0.28",
"pyjwt==2.0.1",
"tensorflow==2.4.1",
"pysftp==0.2.9",
"htmlbuilder==0.2.1",
"vaderSentiment==3.3.2",
"chardet==4.0.0",
"Cython==0.29.17",
"idna==2.9",
"inflection==0.5.1",
"joblib==1.0.1",
"more-itertools==8.7.0",
"numpy==1.19.2",
"ipython==7.21.0",
"pandas==1.2.3",
"pandas-datareader==0.9.0",
"patsy==0.5.1",
"pmdarima==1.8.0",
"python-dateutil==2.8.1",
"python-dotenv==0.15.0",
"pytz==2021.1",
"plotly==4.14.3",
"kaleido==0.2.1",
"Quandl==3.6.1",
"requests==2.25.1",
"scikit-learn==0.24.1",
"torch==1.8.0",
"scipy==1.6.1",
"six==1.15.0",
"statsmodels==0.12.2",
"urllib3==1.26.3",
"xlrd==2.0.1",
"pymongo==3.11.3",
"pysftp==0.2.9",
"md2pdf==0.5",
"sendgrid==6.6.0",
"escapism==1.0.1",
"openpyxl==3.0.7",
"google==3.0.0",
"google-api-python-client==2.0.2",
"google-auth-httplib2==0.1.0",
"google-auth-oauthlib==0.4.3",
"gspread==3.7.0",
"oauth2client==4.1.3",
"geopy==2.1.0",
"GitPython==3.1.14",
"cson==0.8",
"opencv-python==4.5.1.48",
"pytesseract==0.3.7",
"wkhtmltopdf==0.2",

# install by jupyter image
jupyterhub==1.3.0 \
jupyterlab==3.0.10  \
jupyter_client==6.1.11 \
jupyter_server_proxy==1.5.3 \
jupyterlab-git==0.30.0b2 \
nbdime==3.0.0b1  \
nbformat==5.1.2 \
nbconvert==6.0.7 \
flake8==3.8.4 \
jupyter-resource-usage==0.5.1 \
ipyparallel==6.3.0 \
jupyterlab-spellchecker==0.5.1 \
jupyter-archive==3.0.0 \
jupyterlab-tour==3.0.0 \
ipywidgets==7.6.3 \
ipympl==0.6.3 \
jupyterlab_widgets==1.0.0 \
jupyterlab-quickopen==1.0.0 \
jupyterlab-execute-time==2.0.2 \
python-language-server==0.36.2 \
jupyterlab-lsp==3.4.1 \
matplotlib==3.3.4
```

## Jupyter Level

```text
jupyterlab-spreadsheet \
@jupyterlab/server-proxy \
jupyterlab-plotly
```

## Machine Level

```text
redir 
tesseract-ocr
libtesseract-dev
libcairo2-dev
```

## Base image

Below you can find all packages installer by the jupyter team, we use this docker image as base for our own build. 

{% embed url="https://github.com/jupyter/docker-stacks/blob/master/minimal-notebook/Dockerfile" %}

## Naas drivers

In addition to this, we build our machine with naas drivers in it you can check what's is inside below

{% embed url="https://naas.gitbook.io/drivers/installed-librairies" %}



