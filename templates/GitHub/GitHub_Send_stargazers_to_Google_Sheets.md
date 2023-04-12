    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Send_stargazers_to_Google_Sheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Send+stargazers+to+Google+Sheets:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #stars #stargazers #googlesheets #snippet

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to send GitHub stargazers from a given repository to a Google Sheets spreadsheet.

**References:**
- [GitHub - List Stargazers](https://docs.github.com/en/rest/activity/starring?apiVersion=2022-11-28#list-stargazers)
- [Naas drivers - GitHub](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/github.py)
- [Naas drivers - Google Sheets](https://github.com/jupyter-naas/drivers/blob/main/naas_drivers/tools/gsheet.py)

## Input

### Import libraries


```python
from naas_drivers import github, gsheet
import naas
```

### Setup Variables
[Create your GitHub personal access token](https://github.com/settings/tokens)
- `token`: GitHub personal access token
- `repo_url`: URL of the GitHub repository

Share your Google Sheets spreadsheet with our service account : 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com
- `spreadsheet_url`: URL of the Google Sheets spreadsheet
- `sheet_name`: name of the sheet to send data


```python
# Inputs
token = naas.secret.get("GITHUB_TOKEN") or "YOUR_GITHUB_TOKEN"
repo_url = "https://github.com/jupyter-naas/awesome-notebooks"

# Outputs
spreadsheet_url = "https://docs.google.com/spreadsheets/d/1Bk0LgCmdz_Uxxxxxxxxxxxx/edit#gid=0"
sheet_name = "GITHUB_STARGAZERS"
```

## Model

### Get stargazers


```python
df = github.connect(token).repos.get_stargazers(repo_url)
print('Row fetched:', len(df))
df.tail(3)
```

## Output

### Send dataframe to Google Sheets


```python
gsheet.connect(spreadsheet_url).send(
    sheet_name=sheet_name,
    data=df,
    append=False
)
```
