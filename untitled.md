# index

![Naas](https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160)

## LinkedIn - Get comments from post

 [![](https://img.shields.io/badge/-Open%20in%20Naas-success?labelColor=000000&logo=data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTAyNHB4IiBoZWlnaHQ9IjEwMjRweCIgdmlld0JveD0iMCAwIDEwMjQgMTAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIj4KIDwhLS0gR2VuZXJhdGVkIGJ5IFBpeGVsbWF0b3IgUHJvIDIuMC41IC0tPgogPGRlZnM+CiAgPHRleHQgaWQ9InN0cmluZyIgdHJhbnNmb3JtPSJtYXRyaXgoMS4wIDAuMCAwLjAgMS4wIDIyOC4wIDU0LjUpIiBmb250LWZhbWlseT0iQ29tZm9ydGFhLVJlZ3VsYXIsIENvbWZvcnRhYSIgZm9udC1zaXplPSI4MDAiIHRleHQtZGVjb3JhdGlvbj0ibm9uZSIgZmlsbD0iI2ZmZmZmZiIgeD0iMS4xOTk5OTk5OTk5OTk5ODg2IiB5PSI3MDUuMCI+bjwvdGV4dD4KIDwvZGVmcz4KIDx1c2UgaWQ9Im4iIHhsaW5rOmhyZWY9IiNzdHJpbmciLz4KPC9zdmc+Cg==)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_comments_from_post.ipynb)

### Input

```python
from naas_drivers import linkedin
```

#### Get your cookies

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = 'YOUR_COOKIE_LI_AT'  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = 'YOUR_COOKIE_JSESSIONID'  # EXAMPLE ajax:8379907400220387585
```

#### Enter post URL

```python
POST_URL = "POST_URL"
```

### Model

Get the information return in a dataframe.  
  
 **Available columns :**

* PROFILE\_URN : LinkedIn unique profile id
* PROFILE\_ID : LinkedIn public profile id
* FIRSTNAME
* LASTNAME
* TEXT
* OCCUPATION
* ACTIVITY\_COMMENTS
* ACTIVITY\_LIKES
* DISTANCE
* POST\_URL

```python
df = linkedin.connect(LI_AT, JSESSIONID).post.get_comments(POST_URL)
```

### Output

#### Display result

```python
df
```

