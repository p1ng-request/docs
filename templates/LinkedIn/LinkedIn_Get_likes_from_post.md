# Get likes from post

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_likes\_from\_post.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+likes+from+post:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #post #likes #naas\_drivers #content #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides tips and tricks to help you get more likes on your LinkedIn posts.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
```

#### Setup LinkedIn

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585
```

#### Enter post URL

```python
POST_URL = "POST_URL"
```

### Model

Get the information return in a dataframe.\
\
**Available columns :**

* PROFILE\_ID : LinkedIn unique profile ID
* PROFILE\_URL : LinkedIn unique profile URL
* PUBLIC\_ID : LinkedIn public profile ID
* FIRSTNAME : First name of profile
* LASTNAME : Last name of profile
* FULLNAME : First name + Last name
* OCCUPATION : Headline in profile description
* PROFILE\_PICTURE : Profile picture URL
* BACKGROUND\_PICTURE : Background picture URL
* REACTION\_TYPE : Post reaction type
* POST\_URL : Post URL

```python
df = linkedin.connect(LI_AT, JSESSIONID).post.get_likes(POST_URL)
```

### Output

#### Display result

```python
df
```
