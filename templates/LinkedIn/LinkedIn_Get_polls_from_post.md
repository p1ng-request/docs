# Get polls from post

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn\_Get\_polls\_from\_post.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=LinkedIn+-+Get+polls+from+post:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #linkedin #post #polls #naas\_drivers #content #analytics #image #html #plotly

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook allows users to get poll results from their LinkedIn posts.

Disclaimer:\
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by Linkedin or any of its affiliates or subsidiaries. It uses an independent and unofficial API. Use at your own risk.

This project violates Linkedin's User Agreement Section 8.2, and because of this, Linkedin may (and will) temporarily or permanently ban your account. We are not responsible for your account being banned.\


### Input

#### Import libraries

```python
from naas_drivers import linkedin
import plotly.express as px
```

#### Get your cookies

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

#### Get poll results from post

```python
df = linkedin.connect(LI_AT, JSESSIONID).post.get_polls(POST_URL)
print("📝 Nb of poll results", len(df))
df.head(5)
```

### Output

#### Save your result in csv

```python
df.to_csv("POLL.csv", index=False)
print("💾 Poll results saved in csv")
```

#### Create, export and share your graph

```python
def create_polls_graph(df):
    poll_id = df.POLL_ID.unique()[0]
    title = df.POLL_QUESTION.unique()[0]

    # Create dataframe
    df = df.groupby(["POLL_RESULT"], as_index=False).agg({"PROFILE_ID": "count"})
    df["VALUE"] = df["PROFILE_ID"] / df["PROFILE_ID"].sum() * 100
    df["VALUE_D"] = df["VALUE"].map("{:.0f}%".format)

    # Count voters
    voters = df.PROFILE_ID.sum()

    # Create fig
    fig = px.bar(
        df,
        y="POLL_RESULT",
        x="PROFILE_ID",
        orientation="h",
        title=f"{title}<br><span style='font-size: 13px;'>Total amount of votes: {voters}</span>",
        text="VALUE_D",
        labels={
            "POLL_RESULT": "Options",
            "PROFILE_ID": "Nb of votes",
            "VALUE_D": "% of votes",
        },
    )
    fig.update_traces(marker_color="black")
    fig.update_layout(
        plot_bgcolor="#ffffff",
        width=600,
        height=400,
        font=dict(family="Arial", size=14, color="black"),
        paper_bgcolor="white",
        xaxis_title=None,
        xaxis_showticklabels=False,
        yaxis_title=None,
        margin_pad=10,
    )
    fig.write_html(f"{poll_id}.html")
    fig.show()
    asset = naas.asset.add(f"{poll_id}.html")
    return asset


create_polls_graph(df)
```
