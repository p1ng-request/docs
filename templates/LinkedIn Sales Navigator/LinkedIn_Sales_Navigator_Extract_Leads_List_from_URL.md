<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn%20Sales%20Navigator/LinkedIn_Sales_Navigator_Extract_Leads_List_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+Sales+Navigator+-+Extract+Leads+List+from+URL:+Error+short+description">Bug report</a>

**Tags:** #linkedin #salesnavigator #extract #leads

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to extract a list of leads from a URL using LinkedIn Sales Navigator.

**References:**
- [LinkedIn Sales Navigator Documentation](https://docs.microsoft.com/en-us/linkedin/sales-navigator/)
- [LinkedIn Sales Navigator API](https://docs.microsoft.com/en-us/linkedin/sales-navigator/api-overview)

## Input

### Import libraries


```python
from naas_drivers import linkedin_salesnavigator as linkedin_sn
import naas
```

### Setup Variables
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>
- `li_at`: Cookie used to authenticate Members and API clients
- `JSESSIONID`: Cookie used for Cross Site Request Forgery (CSRF) protection and URL signature validation
- `li_a`: Cookie used to authenticate enterprise users on Sales Navigator and Recruiter
- `url`: URL of the page to extract leads from
- `limit`: By default limit is set to 1000
- `csv_output`: Name of the CSV file to be saved. If name is not changed "LINKEDIN_LEADS.csv", we will save it by adding the search ID.


```python
# Inputs
li_at = naas.secret.get("LINKEDIN_LI_AT") or 'ENTER_YOUR_COOKIE_LI_AT_HERE'  # Used to authenticate Members and API clients
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID") or 'ENTER_YOUR_COOKIE_JSESSIONID_HERE'  # Used for Cross Site Request Forgery (CSRF) protection and URL signature validation.
li_a =  naas.secret.get("LINKEDIN_LI_A") or 'ENTER_YOUR_COOKIE_LI_A_HERE'  # Used to authenticate enterprise users on Sales Navigator and Recruiter
url = input("LinkedIn URL:")
limit = 1000

# Outputs
csv_output = "LINKEDIN_LEADS.csv"
```

## Model

### Extract leads from URL
Return an dataframe object with 27 columns:
- PROFILE_ID                    
- PROFILE_URL                   
- FIRSTNAME                     
- LASTNAME                      
- FULLNAME                      
- LOCATION                      
- DISTANCE                      
- PENDING_INVITATIONS           
- PREMIUM                       
- ABOUT                         
- HIGHLIGHTS                    
- PROFILE_PICTURE               
- JOB_TITLE                     
- JOB_DESCRIPTION               
- JOB_START                     
- JOB_TENURE         
- JOB_TENURE_MONTHS
- COMPANY_NAME                  
- COMPANY_ID                    
- COMPANY_LK_URL                
- COMPANY_TENURE      
- COMPANY_TENURE_MONTHS
- COMPANY_INDUSTRY              
- COMPANY_LOGO                  
- SHARED_CONNECTIONS_COUNT
- SHARED_CONNECTIONS


```python
df_leads = linkedin_sn.connect(li_at, JSESSIONID, li_a).leads.get_list(url, limit=limit)
print("Leads Extracted:", len(df_leads))
df_leads.head(3)
```

## Output

### Save dataframe in CSV


```python
def save_df_to_csv(df, csv_output):
    if csv_output ==  "LINKEDIN_LEADS.csv":
        query = url.split("query=")[-1].split("&")[0]
        query_id = urllib.parse.unquote(query).split('recentSearchParam:(id:')[-1].split(",")[0]
        csv_output = f"LINKEDIN_LEADS_{query_id}.csv"
    df.to_csv(csv_output, index=False)
    print('Dataframe successfully saved:', csv_output)
    
save_df_to_csv(df_leads, csv_output)
```
