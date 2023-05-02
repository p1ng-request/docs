<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/BeautifulSoup/BeautifulSoup_List_social_network_links_from_website.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=BeautifulSoup+-+List+social+network+links+from+website:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #beautifulsoup #webscraping #python #html #css #url

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will use BeautifulSoup to list all the social network links from a website. It is usefull for organizations to quickly get a list of all the social networks they are present on.

**References:**
- [BeautifulSoup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

## Input

### Import libraries


```python
import requests
from bs4 import BeautifulSoup
```

### Setup Variables
- `url`: The URL of the website you want to extract social network links from
- `social_network_links`: List of social network links extracted from website


```python
# Inputs
url = "https://www.naas.ai/"

# Outputs
social_network_links = []
```

## Model

### Get social network links


```python
def get_social_network_links(url, social_network_links):
    # Make a GET request to the URL and get the HTML content
    response = requests.get(url)
    html_content = response.text

    # Create a BeautifulSoup object to parse the HTML content
    soup = BeautifulSoup(html_content, 'html.parser')

    # Find all the links on the page
    links = soup.find_all('a')

    # Loop through the links and find the social network links
    social_networks = ['facebook', 'twitter', 'linkedin', 'instagram', 'github', 'youtube']
    for link in links:
        href = link.get('href')
        if href:
            if "github" in href:
                org = href.split("github.com/")[-1].split("/")[0]
                if org not in ["orgs", "sponsors"]:
                    href = f'https://github.com/{org}'
                else:
                    href = ""
            for social in social_networks:
                if social in href:   
                    if href not in social_network_links:
                        social_network_links.append(href)
    return social_network_links
```

## Output

### Display the social network links


```python
social_network_links = get_social_network_links(url, social_network_links)
social_network_links
```

 
