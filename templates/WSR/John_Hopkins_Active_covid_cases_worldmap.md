<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# WSR - John Hopkins Active covid cases worldmap
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WSR/John_Hopkins_Active_covid_cases_worldmap.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

## Input


```python
pip install dataprep --user
```

### Import libraries


```python
import naas
import pandas as pd
import pandas as pd
import plotly.express as px
import plotly.graph_objects as go
import matplotlib.pyplot as plt
from dataprep.clean import clean_country

```

### Setup chart title and date


```python
title = "COVID 19 - Active cases (in milions)"
date = '2022-01-20'
```

### Variables


```python
# URLs of the raw csv dataset
urls = [
    'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv',
    'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv',
    'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_recovered_global.csv'
]

confirmed_df, deaths_df, recovered_df = tuple(pd.read_csv(url) for url in urls)

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```


```python
confirmed_df
```


```python
title = "Worldmap"

# Output paths
output_image = f"{title}.png"
output_html = f"{title}.html"
```

## Model

### Reference
Mostly adopted from this [COVID19 Data Processing Tutorial](https://towardsdatascience.com/covid-19-data-processing-58aaa3663f6)

Clean the dataset to show the cases by country


### Convert all datetimes to a single column


```python
#Wide to Long DataFrame conversion
dates = confirmed_df.columns[4:]
confirmed_df_long = confirmed_df.melt(
    id_vars=['Province/State', 'Country/Region', 'Lat', 'Long'], 
    value_vars=dates, 
    var_name='Date', 
    value_name='Confirmed'
)
deaths_df_long = deaths_df.melt(
    id_vars=['Province/State', 'Country/Region', 'Lat', 'Long'], 
    value_vars=dates, 
    var_name='Date', 
    value_name='Deaths'
)
recovered_df_long = recovered_df.melt(
    id_vars=['Province/State', 'Country/Region', 'Lat', 'Long'], 
    value_vars=dates, 
    var_name='Date', 
    value_name='Recovered'
)

# Adjust for Canada
recovered_df_long = recovered_df_long[(recovered_df_long['Country/Region']!='Canada')]
```

### Merge tables into a single table


```python
# Join into one single dataframe/table
# Merging confirmed_df_long and deaths_df_long
full_table = confirmed_df_long.merge(
  right=deaths_df_long, 
  how='left',
  on=['Province/State', 'Country/Region', 'Date', 'Lat', 'Long']
)
# Merging full_table and recovered_df_long
full_table = full_table.merge(
  right=recovered_df_long, 
  how='left',
  on=['Province/State', 'Country/Region', 'Date', 'Lat', 'Long']
)

# Convert date strings to actual dates
full_table['Date'] = pd.to_datetime(full_table['Date'])
# Handle some missing values / NaNs
full_table['Recovered'] = full_table['Recovered'].fillna(0).astype('int64')


```


```python
full_table.isna().sum()
# full_table.dtypes
full_table
```

### Adjust covid cases for cruise ships and Canada 


```python
# Adjust for Canada and 3 cruise ships
ship_rows = full_table['Province/State'].str.contains('Grand Princess') | full_table['Province/State'].str.contains('Diamond Princess') | full_table['Country/Region'].str.contains('Diamond Princess') | full_table['Country/Region'].str.contains('MS Zaandam')
full_ship = full_table[ship_rows]
full_table = full_table[~(ship_rows)]

# Add one more entry for each day to get the entire world's counts/totals
world_dict = {"Country/Region": "World", "Confirmed": pd.Series(full_table.groupby(['Date'])['Confirmed'].sum()), "Deaths": pd.Series(full_table.groupby(['Date'])['Deaths'].sum()),"Recovered": pd.Series(full_table.groupby(['Date'])['Recovered'].sum())}
world_df = pd.DataFrame.from_dict(world_dict).reset_index()
print(world_df.columns)
full_table = pd.concat([full_table, world_df], ignore_index=True)
```

### Calculate Active Cases 


```python
full_table['Active'] = full_table['Confirmed'] - full_table['Deaths'] - full_table['Recovered']
full_grouped= full_table.groupby(['Date', 'Country/Region'])['Active'].sum().reset_index()
full_grouped.rename(columns = {'Date':'DATE'}, inplace = True)
full_grouped.rename(columns = {'Country/Region':'COUNTRY'}, inplace = True)
full_grouped.rename(columns = {'Active':'ACTIVE'}, inplace = True)

full_grouped
```


```python
df = pd.DataFrame(full_grouped)
df2 = clean_country(df, 'COUNTRY', output_format='alpha-3')
df2.rename(columns = {'COUNTRY_clean':'ISO'}, inplace = True)

df2
```

### Filter unecessary rows


```python
# filter 
newdf = df2[(df2.COUNTRY) != 'World']
df = newdf[(newdf.DATE) == date]
df
```

## Output

### Create chart


```python
fig = go.Figure()

config = {'displayModeBar': False}

fig = go.Figure(data=go.Choropleth(
    locations = df['ISO'],
    z = df['ACTIVE'],
    text = df['COUNTRY'],
    colorscale = 'Blues',
    autocolorscale=False,
    reversescale=False,
    marker_line_color='darkgray',
    marker_line_width=0.5,
    colorbar_tickprefix = '',
    colorbar_title = 'Active cases',
))

fig.update_layout(
    title=title ,
    plot_bgcolor="#ffffff",
    legend_x=1,
    geo=dict(
        showframe=False,
        showcoastlines=False,
        #projection_type='equirectangular'
    ),
    dragmode= False,
    #width=800,
    height=600,

)
fig.show(config=config)
```
