<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# HubSpot - Get new deals created weekly
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/HubSpot/HubSpot_Get_new_deals_created_weekly.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #hubspot #crm #sales #deal #naas_drivers #scheduler #asset

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

## Input


```python
#-> Uncomment the 2 lines below (by removing the hashtag) to schedule your job everyday at 8:00 AM (NB: you can choose the time of your scheduling bot)
# import naas
# naas.scheduler.add(cron="0 8 * * *")

#-> Uncomment the line below (by removing the hashtag) to remove your scheduler
# naas.scheduler.delete()
```

### Import libraries


```python
from naas_drivers import hubspot
from datetime import timedelta
import pandas as pd
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

### Setup your HubSpot
👉 Access your [HubSpot API key](https://knowledge.hubspot.com/integrations/how-do-i-get-my-hubspot-api-key)


```python
HS_API_KEY = 'YOUR_HUBSPOT_API_KEY'
```

### Select your pipeline ID
Here below you can select your pipeline.<br>
If not, all deals will be taken for the analysis


```python
df_pipelines = hubspot.connect(HS_API_KEY).pipelines.get_all()
df_pipelines
```


```python
pipeline_id = None
```

## Model

### Get all deals


```python
df_deals = hubspot.connect(HS_API_KEY).deals.get_all()
df_deals
```

### Create trend data


```python
def get_trend(df_deals, pipeline=None):
    df = df_deals.copy()
    # Filter data
    if pipeline is not None:
        df = df[df["pipeline"].astype(str) == str(pipeline)]
    
    # Prep data
    df["createdate"] = pd.to_datetime(df["createdate"])
    df["amount"] = df.apply(lambda row: float(row["amount"]) if str(row["amount"]) not in ["None", ""] else 0, axis=1)
    
    # Calc by week
    df = df.groupby(pd.Grouper(freq='W', key='createdate')).agg({"hs_object_id": "count", "amount": "sum"}).reset_index()
    df["createdate"] = df["createdate"] + timedelta(days=-1)
    df = pd.melt(df, id_vars="createdate")
    
    # Rename col
    to_rename = {
        "createdate": "LABEL_ORDER",
        "variable": "GROUP",
        "value": "VALUE"
    }
    df = df.rename(columns=to_rename).replace("hs_object_id", "No of deals").replace("amount", "Amount")
    df["LABEL"] = df["LABEL_ORDER"].dt.strftime("%Y-W%U")
    df["LABEL_ORDER"] = df["LABEL_ORDER"].dt.strftime("%Y%m%d")
    
    # Calc variation
    df_var = pd.DataFrame()
    groups = df.GROUP.unique()
    for group in groups:
        tmp = df[df.GROUP == group].reset_index(drop=True)
        for idx, row in tmp.iterrows():
            if idx == 0:
                value_n1 = 0
            else:
                value_n1 = tmp.loc[tmp.index[idx-1], "VALUE"]
            tmp.loc[tmp.index[idx], "VALUE_COMP"] = value_n1
        df_var = pd.concat([df_var, tmp])
    df_var["VARV"] = df_var["VALUE"] - df_var["VALUE_COMP"]
    df_var["VARP"] = df_var["VARV"] / abs(df_var["VALUE_COMP"])
    return df_var.fillna(0).reset_index(drop=True)

df_trend = get_trend(df_deals, "8432671")
df_trend
```

## Output

### Plotting a barchart with filters


```python
def create_barchart(df, label, group, value, varv, varp):
    # Get last value
    df["VALUE_D"] = df[value].map("{:,.0f}".format).str.replace(",", " ")
    df["VARV_D"] = df[varv].map("{:,.0f}".format).str.replace(",", " ")
    df.loc[df[varv] > 0, "VARV_D"] = "+" + df["VARV_D"]
    df["VARP_D"] = df[varp].map("{:,.0%}".format).str.replace(",", " ")
    df.loc[df[varp] > 0, "VARP_D"] = "+" + df["VARP_D"]
    
    # Create hovertext
    df["TEXT"] = ("<b>Deal created as of " + df[label] + " : </b>" + 
                  df["VALUE_D"] + "<br>" + 
                  df["VARP_D"] + " vs last week (" + df["VARV_D"] + ")")
    
    # Create figure with secondary y-axis
    fig = make_subplots(specs=[[{"secondary_y": True}]])

    # Add traces
    df1 = df[df[group] == "No of deals"].reset_index(drop=True)[-12:]
    fig.add_trace(
        go.Bar(
            name="No of deals",
            x=df1[label],
            y=df1[value],
            offsetgroup=0,
            hoverinfo="text",
            hovertext=df1["TEXT"],
            marker=dict(color="blue")
        ),
        secondary_y=False,
    )
    
    df2 = df[df[group] == "Amount"].reset_index(drop=True)[-12:]
    fig.add_trace(
        go.Bar(
            name="Amount",
            x=df2[label],
            y=df2[value],
            offsetgroup=1,
            hoverinfo="text",
            hovertext=df2["TEXT"],
            marker=dict(color="orange")
        ),
        secondary_y=True,
    )

    # Add figure title
    fig.update_layout(
        title=f"<b>Hubspot - Deals created last 12 weeks</b><br><span style='font-size: 13px;'></span>",
        title_font=dict(family="Arial", size=18, color="black"),
        legend=None,
        plot_bgcolor="#ffffff",
        width=1200,
        height=800,
        paper_bgcolor="white",
        xaxis_title="Weeks",
        xaxis_title_font=dict(family="Arial", size=11, color="black"),
    )

    # Set y-axes titles
    fig.update_yaxes(
        title_text="No of deals",
        title_font=dict(family="Arial", size=11, color="black"),
        secondary_y=False
    )
    fig.update_yaxes(
        title_text="Amount in K€",
        title_font=dict(family="Arial", size=11, color="black"),
        secondary_y=True
    )

    fig.show()
    return fig

fig = create_barchart(df_trend, "LABEL", "GROUP", "VALUE", "VARV", "VARP")
```

### Export and share graph


```python
# Export in HTML
fig.write_html(html_output)

# Shave with naas
#-> Uncomment the line below (by removing the hashtag) to share your asset with naas
# naas.asset.add(html_output, params={"inline": True})

#-> Uncomment the line below (by removing the hashtag)  to delete your asset
# naas.asset.delete(html_output)
```
