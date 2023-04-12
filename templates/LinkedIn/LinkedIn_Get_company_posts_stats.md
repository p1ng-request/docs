    <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn_Get_company_posts_stats.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LinkedIn+-+Get+company+posts+stats:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #linkedin #company #post #stats #naas_drivers #content #automation #csv

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook provides an analysis of company posts on LinkedIn, including statistics and insights.

## Input

### Import libraries


```python
from naas_drivers import linkedin
import pandas as pd
from datetime import datetime
import naas
```

### Setup LinkedIn
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
# LinkedIn cookies
LI_AT = (
    naas.secret.get("LI_AT") or "ENTER_YOUR_COOKIE_HERE"
)  # EXAMPLE : "AQFAzQN_PLPR4wAAAXc-FCKmgiMit5FLdY1af3-2"
JSESSIONID = (
    naas.secret.get("JSESSIONID") or "ENTER_YOUR_JSESSIONID_HERE"
)  # EXAMPLE : "ajax:8379907400220387585"

# LinkedIn profile url
COMPANY_URL = "ENTER_YOUR_LINKEDIN_COMPANY_URL_HERE"  # EXAMPLE "https://www.linkedin.com/company/XXXXXX/"
```

### Setup Outputs
Create CSV to store your posts stats.<br>
PS: This CSV could be used in others LinkedIn templates.


```python
# Custom path of your CSV with the company URL
company_id = COMPANY_URL.split("https://www.linkedin.com/company/")[-1].split("/")[0]
csv_output = f"LINKEDIN_POSTS_{company_id}.csv"
```

### Setup Naas scheduler
Schedule your notebook with the naas scheduler feature


```python
# the default settings below will make the notebook run everyday at 8:00
# for information on changing this setting, please check https://crontab.guru/ for information on the required CRON syntax
naas.scheduler.add(cron="0 8 * * *")

# to de-schedule this notebook, simply run the following command:
# naas.scheduler.delete()
```

## Model

### Get your posts from CSV
All your posts will be stored in CSV.


```python
def read_csv(file_path):
    try:
        df = pd.read_csv(file_path)
    except FileNotFoundError as e:
        # Empty dataframe returned
        return pd.DataFrame()
    return df


df_posts = read_csv(csv_output)
df_posts
```

### Update last posts
This function will only update the last 5 posts from LinkedIn API.<br>
To change this parameters you can set another number to the parameter "no_posts" in the update_posts() function.

PS: On the first execution all posts will be retrieved.


```python
def update_posts(
    df_posts, company_url, key="POST_URL", no_posts=5, min_updated_time=60
):
    # Init output
    df = pd.DataFrame()
    df_new = pd.DataFrame()

    # Init df posts is empty then return entire database
    if len(df_posts) > 0:
        if "DATE_EXTRACT" in df_posts.columns:
            last_update_date = df_posts["DATE_EXTRACT"].max()
            time_last_update = datetime.now() - datetime.strptime(
                last_update_date, "%Y-%m-%d %H:%M:%S"
            )
            minute_last_update = time_last_update.total_seconds() / 60
            if minute_last_update > min_updated_time:
                # If df posts not empty get the last X posts (new and already existing)
                df_new = linkedin.connect(LI_AT, JSESSIONID).company.get_posts_feed(
                    company_url, limit=no_posts
                )
            else:
                print(
                    f"🛑 Nothing to update. Last update done {int(minute_last_update)} minutes ago."
                )
    else:
        df_new = linkedin.connect(LI_AT, JSESSIONID).company.get_posts_feed(
            company_url, limit=-1
        )

    # Concat, save database in CSV and dependency in production
    df = pd.concat([df_new, df_posts]).drop_duplicates(key, keep="first")

    # Return all posts
    print(f"✅ Updated posts fetched:", len(df))
    return df.reset_index(drop=True)


df_update = update_posts(df_posts, COMPANY_URL)
df_update.head(1)
```

## Output

### Save dataframe in CSV and send to production


```python
# Save dataframe in CSV
df_update.to_csv(csv_output, index=False)

# Send CSV to production (It could be used with other scripts)
naas.dependency.add(csv_output)
```
