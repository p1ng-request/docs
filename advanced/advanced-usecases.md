# Advanced use cases

## Timezone

If you are located in other countries than France, use those formulas to set up the time zone according to [your country's ISO code](https://timezonedb.com/time-zones).

### Set timezone

```python
import naas
naas.set_remote_timezone("Europe/Lisbon")
```

### Get timezone

```python
import naas
naas.get_remote_timezone()
```

## Whitelist Naas&#x20;

If you want to enable Naas to access your infrastructure. Here are the IPs to whitelist:

* 15.236.83.113
* 15.236.82.50
* 15.236.53.238

## Download URL

Create a download link to Naas from any URL, it can be in GitHub, or anywhere!

```python
import naas
url = "https://github.com/jupyter-naas/awesome-notebooks/blob/master/Airtable/Airtable_delete_data.ipynb"
dl_url = naas.get_download_url(url)
```

Result :

![](<../.gitbook/assets/image (5) (1) (1) (1) (1).png>)

```
https://app.naas.ai/user-redirect/naas/downloader?url=YOURURL
```

{% hint style="info" %}
Options: mode\_api&#x20;

with \&mode\_api=yes that create the file in the user but don't open it. Useful for admin&#x20;
{% endhint %}

{% hint style="info" %}
Options: name&#x20;

with ?name=toto that create a file in the user with the name provided \`toto\`

&#x20;if no URL provided it create an empty file.&#x20;
{% endhint %}

## Run

Run a notebook direct in production and get the result.

```python
import naas
naas.run()
```

## Changelog (deprecated)

Show changelog&#x20;

```python
import naas
naas.changelog()
```

## Feature request (deprecated)

show feature request inside Jupyter

```python
import naas
mode = "naas" # can be naas, naas_drivers, awesome_notebook
naas.feature_request(mode)
```

## Check if you are in production

```python
import naas

naas.is_production()
```

## Reload jobs

If you need to force update the job list by editing the file in your \`.naas/jobs.json\`

```python
import naas

naas.reload_jobs()
```

## N\_ENV

This represents the Naas env vars, you can get all to make your script work \`naas.n\_env\`

```
api_port
current
version
remote_mode
api
notif_api
callback_api
proxy_api
hub_api
any_user_url
user_url
naas_folder
server_root
path_naas_folder
shell_user
remote_api
token
user
tz
sentry_dsn
scheduler
scheduler_interval
scheduler_job_max
scheduler_job_name
scheduler_timeout
```

### Current

get data in the production of the current running notebook.

For now current gives you this :

![](<../.gitbook/assets/image (4).png>)

```python
import naas
print(naas.n_env.current)
# This will be empty in dev = in notebook run by you
# and with vars when run by naas runner ( scheduler or webhook )
```
