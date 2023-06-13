<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Advertools/Advertools_Analyze_website_content_using_XML_sitemap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Advertools+-+Analyze+website+content+using+XML+sitemap:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #advertools #xml #sitemap #website #analyze #seo

**Author:** [Elias Dabbas](https://www.linkedin.com/in/eliasdabbas/)

**Description:** This notebook helps you get an overview of a website's content by analyzing and visualizing its XML sitemap. It's also an important SEO audit process that can uncover some potential issues that might affect the website.

**References:**
- [advertools Sitemaps](https://advertools.readthedocs.io/en/master/advertools.sitemaps.html)
- [XML Sitemap](https://www.xml-sitemaps.com/)
- [Sitemaps Protocol](https://www.sitemaps.org/)

## Input

### Import libraries


```python
try:
    import advertools as adv
except:
    !pip install advertools --user
    import advertools as adv
try:
    import adviz
except:
    !pip install adviz --user
    import adviz
from urllib.parse import urlsplit
```

### Setup Variables
- `sitemap_url`: URL of the sitemap to analyze, which can be
    * The URL of an XML sitemap
    * The URL of an XML sitemapindex
    * The URL of a robots.txt file
    * Normal and zipped formats are supported
- `recursive`: If this is a sitemapindex, should all the sub-sitemaps also be  downloaded, parsed and combined into one DataFrame?
- `max_workers`: Number of concurrent workers to fetch the sitemaps.


```python
sitemap_url = "https://www.xml-sitemaps.com/download/www.naas.ai-a2e8849ba/sitemap.xml?view=1"
recursive = True
max_workers = 8
```

## Model

### Analyze website content using XML sitemap
Getting the sitemap(s)


```python
sitemap = adv.sitemap_to_df(
    sitemap_url=sitemap_url,
    max_workers=max_workers,
    recursive=recursive
)
sitemap
```

Split URLs into their components for further analysis/understanding


```python
urldf = adv.url_to_df(sitemap['loc'])
urldf
```

## Output

### Display results

#### Errors


```python
if 'errors' in sitemap:
    from IPython.display import display
    display(sitemap[sitemap['errors'].notnull()])
else:
    print('No errors found')
```

#### Duplicated URLs


```python
duplicated = sitemap[sitemap['loc'].duplicated()]
if not duplicated.empty:
    display(duplicated)
else:
    print('No duplicated URLs found')
```

#### URL counts per sitemap and sitemap sizes

Each sitemap should have a maximumof 50,000 URLs, and its size should not exceek 50MB

URL counts:


```python
adviz.value_counts_plus(sitemap['sitemap'], name='Sitemap URLs')
```

URL Sizes:


```python
sitemap['sitemap_size_mb'].describe().to_frame().T.style.format('{:,.2f}')
```

#### Count unique values of URL components


```python
for col in ['scheme', 'netloc', 'dir_1', 'dir_2', 'dir_3']:
    try:
        display(adviz.value_counts_plus(urldf[col], name=col))
    except Exception as e:
        continue
```

#### Visualize the structure of the URLs


```python
domain = urlsplit(sitemap_url).netloc
try:
    adviz.url_structure(
        urldf['url'].fillna(''),
        items_per_level=30,
        domain=domain,
        height=750,
        title=f'URL Structure: {domain} XML sitemap'
    )
except Exception as e:
    print(str(e))
    pass
```
