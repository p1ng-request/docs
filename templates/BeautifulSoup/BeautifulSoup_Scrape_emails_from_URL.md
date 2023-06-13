<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/BeautifulSoup/BeautifulSoup_Scrape_emails_from_URL.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=BeautifulSoup+-+Scrape+emails+from+URL:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #beautifulsoup #python #scraping #emails #url #webscraping #html

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to scrape emails stored in HTML webpage using BeautifulSoup.

<u>References:</u>
- [Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Regular Expression Documentation](https://docs.python.org/3/library/re.html)

## Input

### Import libraries


```python
import re
import requests
from urllib.parse import urlsplit
from collections import deque
from bs4 import BeautifulSoup
import pandas as pd
```

### Setup Variables
- `url`: URL of the webpage to scrape
- `limit`: number of emails found to stop scraping


```python
url = "https://www.naas.ai/"
limit = 3
```

## Model

### Scrape emails from URL

We will use the `requests` library to get the HTML content of the webpage and the `BeautifulSoup` library to parse the HTML content. We will use a regular expression to extract the emails from the HTML content.


```python
unscraped = deque([url])  

scraped = set()  

emails = set()  

while len(unscraped):
    url = unscraped.popleft()  
    scraped.add(url)

    parts = urlsplit(url)
        
    base_url = "{0.scheme}://{0.netloc}".format(parts)
    if '/' in parts.path:
        path = url[:url.rfind('/')+1]
    else:
        path = url

    print("Crawling URL: %s" % url)
    try:
        response = requests.get(url)
    except (requests.exceptions.MissingSchema, requests.exceptions.ConnectionError):
        continue
        
    exclude = ["google.com", "gmail.com", "example.com"]    
    # Get emails from URL
    new_emails = re.findall(r"[a-z0-9\.\-+_]+@[a-z0-9\.\-+_]+\.+[a-z]{1,3}", url)
    for email in new_emails:
        for e in exclude:
            if not email.endswith(e):
                emails.update([email])
                
    # Get emails from content
    new_emails = set(re.findall(r"[a-z0-9\.\-+_]+@[a-z0-9\.\-+_]+\.+[a-z]{1,3}", response.text, re.I))
    for email in new_emails:
        for e in exclude:
            if not email.endswith(e):
                emails.update([email])
                
    if len(emails) >= limit:
        break

    soup = BeautifulSoup(response.text, 'lxml')
    for anchor in soup.find_all("a"):
        if "href" in anchor.attrs:
            link = anchor.attrs["href"]
        else:
            link = ''

        if link.startswith('/'):
            link = base_url + link
        
        elif not link.startswith('http'):
            link = path + link

        if not link.endswith(".gz"):
            if not link in unscraped and not link in scraped:
                unscraped.append(link)

print(emails)
```

## Output

### Display result


```python
print(f"🚀 {len(emails)} founded on {url}")
print(emails)
```

 
