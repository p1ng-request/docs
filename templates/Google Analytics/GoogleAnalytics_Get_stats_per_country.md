<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Google%20Analytics/GoogleAnalytics_Get_stats_per_country.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #googleanalytics #statspercountry

Pre-requisite: Create your own <a href="">Google API JSON credential</a>

## Input

### Import library


```python
import pycountry

import plotly.graph_objects as go
import plotly.express as px

from naas_drivers import googleanalytics
```

### Get your credential from Google Cloud Platform


```python
json_path = '/Users/charlesdemontigny/Desktop/naas-335023-90c733ba64dd.json'
```

### Get view id from google analytics


```python
view_id = "236707574"
```

## Model

### Report Website - Google Analytics performance


```python
googleanalytics.connect(json_path=json_path)
```

### Visitor's country of origin


```python
country = googleanalytics.views.get_data(
            view_id,
            metrics="ga:sessions",
            pivots_dimensions="ga:country",
            dimensions="ga:month",
            start_date=None,
            end_date=None,
            format_type="pivot",
        )
```


```python
sessions_per_country = googleanalytics.views.get_country(view_id) # default: metrics="ga:sessions"
```


```python
sessions_per_country
```


```python
users_per_country = googleanalytics.views.get_country(view_id, metrics="ga:users")  
```

## Output

### Display result


```python
sessions_per_country.head()
```


```python
users_per_country.head()
```


```python
sessions_per_country = sessions_per_country.reset_index().rename(columns={"index": "Country"})
mapping = {country.name: country.alpha_3 for country in pycountry.countries}
sessions_per_country['iso_alpha'] = sessions_per_country['Country'].apply(lambda x: mapping.get(x))
```


```python
sessions_per_country
```


```python
fig = px.choropleth(sessions_per_country, locations="iso_alpha",
                    color="Sessions", 
                    hover_name="Country",
                    color_continuous_scale="Greens")
fig.show()
```


```python

```
