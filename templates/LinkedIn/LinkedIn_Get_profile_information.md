# Get profile information

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_profile\_information.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+profile+information:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #profile #resume #naas\_drivers #content #snippet #dataframe

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows you to access and analyze profile information from LinkedIn.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import naas
```

#### Get your cookies

[How to get your cookies ?](https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75)

```python
LI_AT = naas.secret.get("LINKEDIN_LI_AT")
JSESSIONID = naas.secret.get("LINKEDIN_JSESSIONID")
```

#### Enter profile URL

```python
PROFILE_URL = "florent-ravenel"
```

### Model

#### Get identity

```python
df_identity = linkedin.connect(LI_AT, JSESSIONID).profile.get_identity(PROFILE_URL)
df_identity
```

#### Get network

```python
df_network = linkedin.connect(LI_AT, JSESSIONID).profile.get_network(PROFILE_URL)
df_network
```

#### Get contact

```python
df_contact = linkedin.connect(LI_AT, JSESSIONID).profile.get_contact(PROFILE_URL)
df_contact
```

#### Get resume

```python
df_resume = linkedin.connect(LI_AT, JSESSIONID).profile.get_resume(PROFILE_URL)
df_resume
```

### Output

#### Display result
