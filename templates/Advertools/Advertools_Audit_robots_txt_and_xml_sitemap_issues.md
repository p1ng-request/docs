<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Advertools/Advertools_Audit_robots_txt_and_xml_sitemap_issues.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Advertools+-+Audit+robots+txt+and+xml+sitemap+issues:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #advertools #xml #sitemap #website #audit #seo #robots.txt #google

**Author:** [Elias Dabbas](https://www.linkedin.com/in/eliasdabbas/)

**Description:** This notebook helps you check if there are any conflicts between robots.txt rules and your XML sitemap.

* Are you disallowing URLs that you shouldn't?
* Test and make sure you don't publish new pages with such conflicts.
* Do this in bulk: for all URL/rule/user-agent combinations run all tests with one command.

**References:**
- [advertools robots.txt functions](https://advertools.readthedocs.io/en/master/advertools.robotstxt.html)
- [Google's robots reference](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt)
- [advertools XML sitemaps](https://advertools.readthedocs.io/en/master/advertools.sitemaps.html)

## Input

### Import libraries


```python
try:
    import advertools as adv
except ModuleNotFoundError:
    !pip install advertools
    import advertools as adv
```

### Setup Variables
- `robotstxt_url`: URL of the robots.txt file to convert to a `DataFrame`


```python
robotstxt_url = "https://www.example.com/robots.txt"
```

## Model

### Analyze potential robots.txt and XML conflicts

Getting the robots.txt file and converting it to a `DataFrame`.


```python
robots_df = adv.robotstxt_to_df(robotstxt_url=robotstxt_url)
robots_df
```

Get XML sitemap(s) and convert to a `DataFrame`.


```python
sitemap = adv.sitemap_to_df(
    # the function will extract and combine all available sitemaps
    # in the robots.txt file
    robotstxt_url,
    max_workers=8,
    recursive=True)
sitemap
```

#### Testing robots.txt
For all URL/user-agent combinations check if the URL is blocked.


```python
user_agents = robots_df[robots_df['directive'].str.contains('user-agent', case=False)]['content']
user_agents
```

Generate the robots.txt test report:


```python
# Get users agent
user_agents = robots_df[robots_df['directive'].str.contains('user-agent', case=False)]['content']
print(user_agents)

# Testing robots.txt
robots_report = adv.robotstxt_test(
    robotstxt_url=robotstxt_url,
    user_agents=user_agents,
    urls=sitemap['loc'].dropna()
)

print("Row fetched:", len(robots_report))
robots_report.head(5)
```

Does the website have URLs listed in the XML sitemap that are also disallowed by its robots.txt?

(this is not necessarily a problem, because they might disallow it for some user-agents only), and it's good to check.

## Output

Get the URLs that cannot be fetched

### Filter result


```python
df_report = robots_report[~robots_report['can_fetch']].reset_index(drop=True)
print("Row fetched:", len(df_report))
df_report.head(5)
```
