# HTML - Create a website
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HTML/HTML_Create_a_website.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #html #css #website #page #landing #custom

The objective of this notebook is to create an end-to-end website in 5min. 

## Input 


```python
from urllib.request import urlopen
html = urlopen("http://www.example.com/").read().decode('utf-8')
print(html)
```

# Model 

### Save file on your file system
Click right to open + edit the file downloaded 


```python
html_file = open("site.html","w")
html_file.write(html)
html_file.close()
```

### Learn about HTML with this Cheat Sheet


```python
from IPython.display import IFrame
IFrame("https://web.stanford.edu/group/csp/cs21/htmlcheatsheet.pdf", width=900, height=600)
```

### Manually change the content of the file to make it your own. 

Use Google search to go further in the customization (I recommend using https://stackoverflow.com/ + https://www.w3schools.com/html/)

## Output

Use Naas asset formula to generate a shareable URL.


```python
import naas 
naas.asset.add("site.html",{"inline": True})
```

Nb: if you want to use your own domain name, we will cover that in another version of this template.
Contact us → hello@naas.ai


```python

```
