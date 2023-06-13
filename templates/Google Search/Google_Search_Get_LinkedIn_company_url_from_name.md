<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Search/Google_Search_Get_LinkedIn_company_url_from_name.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Google+Search+-+Get+LinkedIn+company+url+from+name:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #googlesearch #snippet #operations #url

**Author:** [Florent Ravenel](https://www.linkedin.com/in/ACoAABCNSioBW3YZHc2lBHVG0E_TXYWitQkmwog/)

**Description:** This notebook provides a method to quickly obtain the LinkedIn URL of a company from its name using Google Search.

## Input

### Import library


```python
try:
    from googlesearch import search
except:
    !pip install google
    from googlesearch import search
import re
```

### Variables


```python
company = "Tesla"
```

## Model

### Get LinkedIn url


```python
def get_linkedin_url(company):
    # Init linkedinbio
    linkedinbio = None

    # Create query
    query = f"{company}+Linkedin"
    print("Google query: ", query)

    # Search in Google
    for i in search(query, tld="com", num=10, stop=10, pause=2):
        pattern = "https:\/\/.+.linkedin.com\/company\/.([^?])+"
        result = re.search(pattern, i)

        # Return value if result is not None
        if result != None:
            linkedinbio = result.group(0).replace(" ", "")
            return linkedinbio
    return linkedinbio


linkedin_url = get_linkedin_url(company)
```

## Output

### Display the result of the search


```python
linkedin_url
```
