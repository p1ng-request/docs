<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_likes_from_post.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Get+likes+from+post:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #post #likes #naas_drivers #content #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides tips and tricks to help you get more likes on your LinkedIn posts.


<div class="alert alert-info" role="info" style="margin: 10px">
<b>Disclaimer:</b><br>
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.
<br>
</div>

## Input

### Import libraries


```python
from naas_drivers import linkedin
```

### Setup LinkedIn
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
LI_AT = "YOUR_COOKIE_LI_AT"  # EXAMPLE AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2
JSESSIONID = "YOUR_COOKIE_JSESSIONID"  # EXAMPLE ajax:8379907400220387585
```

### Enter post URL


```python
POST_URL = "POST_URL"
```

## Model

Get the information return in a dataframe.<br><br>
**Available columns :**
- PROFILE_ID : LinkedIn unique profile ID
- PROFILE_URL : LinkedIn unique profile URL
- PUBLIC_ID : LinkedIn public profile ID
- FIRSTNAME : First name of profile
- LASTNAME : Last name of profile
- FULLNAME : First name + Last name
- OCCUPATION : Headline in profile description
- PROFILE_PICTURE : Profile picture URL
- BACKGROUND_PICTURE : Background picture URL
- REACTION_TYPE : Post reaction type
- POST_URL : Post URL


```python
df = linkedin.connect(LI_AT, JSESSIONID).post.get_likes(POST_URL)
```

## Output

### Display result


```python
df
```
