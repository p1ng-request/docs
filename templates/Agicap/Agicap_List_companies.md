<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Agicap/Agicap_List_companies.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Agicap+-+List+companies:+Error+short+description">Bug report</a>

**Tags:** #agicap #companies #accountingsoftware #financialmanagement #businessmanagement #financetracking #budgetplanning #invoicing #expensetracking #businessinsights #dataanalysis

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook lists all the companies within Agicap with their IDs.

<u>References</u>:
- https://www.postman.com/agicap-data-int/workspace/agicap-public/documentation/16057249-07e739b2-d2f7-4437-82fa-7ca0d290336b

**About AGICAP?**

Agicap is a powerful accounting software for managing your company's finances. It offers features such as expense tracking, budget planning, invoicing, and data analysis to help you make informed business decisions.

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Agicap
Agicap public API uses token-based authentification method.

To start using the API, you need first to generate an API token within your Agicap dashboard.
- Go to the API section of your advance settings page by following this [link](https://app.agicap.com/fr/app/parametres/openapi).
- Click on Generate Token
- Enter a name for your token (useful for remembering its context of use)
- Copy the generated token and save it securely


```python
AGICAP_TOKEN = naas.secret.get("AGICAP_TOKEN") or "eGu3qPIo6kuetXXXXXXXX"
```

## Model

### Retrieve Companies
Now you have generated your API Token, it's time to try it with your first API call.

For this, we are going to start by calling the GET /companies endpoint that allows you to retrieve all the Companies linked to your Agicap account (through your API Token).


```python
url = "https://openapi.agicap.com/api/companies"

# Headers
headers = {
    "Accept": "application/json",
    "Authorization": f"Bearer {token}",
}
# Request
res = requests.get(url, headers=headers)
res.raise_for_status
res
```

## Output

### Tranform json to dataframe


```python
pd.DataFrame(res.json())
```
