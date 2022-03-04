# YahooFinance - Send daily prediction to Slack
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/YahooFinance/YahooFinance_Send_daily_prediction_to_Slack.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #yahoofinance #trading #markdown #prediction #plotly #slack #naas_drivers #scheduler #asset #dependency #naas

With this template, you can create daily Slack prediction bot on any ticker available in YahooFinance.<br> 

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/j%C3%A9r%C3%A9my-ravenel-8a396910/)

## Input

### Import libraries


```python
import naas
from naas_drivers import prediction, yahoofinance, plotly, slack
import markdown2
```

### Input ticker and dates


```python
ticker = "ABNB"
date_from = -900 # 1OO days max to feed the naas_driver for prediction
date_to = "today"
data_point = 20
```

### Input Slack token and channel


```python
token = "your_token_number"
channel = "your_channel_name"
```

## Model

### Get the data from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker, date_from=date_from, date_to=date_to)

# clean df
df_yahoo = df_yahoo.dropna()
df_yahoo.reset_index(drop=True)
df_yahoo.head()
```

### Make prediction chart

#### Predict datapoints


```python
df_predict = prediction.get(dataset=df_yahoo,
                            date_column='Date',
                            data_points=20,
                            prediction_type="all")
```


```python
df_predict = df_predict.sort_values("Date", ascending=False).reset_index(drop=True)
df_predict.head(30)
```

#### Build chart


```python
chart = plotly.linechart(df_predict,
                         x="Date",
                         y=["Close", "ARIMA", "SVR", "LINEAR", "COMPOUND"],
                         showlegend=True,
                         title=f"{ticker} predictions as of today, for next {data_point} days.")
```

#### Display predicted values


```python
ARIMA = df_predict.loc[0, "ARIMA"]
ARIMA = round(ARIMA, 1)
ARIMA = "${:,.2f}".format(ARIMA)
ARIMA
```


```python
SVR = df_predict.loc[0, "SVR"]
SVR = round(SVR, 1)
SVR = "${:,.2f}".format(SVR)
SVR
```


```python
LINEAR = df_predict.loc[0, "LINEAR"]
LINEAR = round(LINEAR, 1)
LINEAR = "${:,.2f}".format(LINEAR)
LINEAR
```


```python
COMPOUND = df_predict.loc[0, "COMPOUND"]
COMPOUND = round(COMPOUND, 1)
COMPOUND = "${:,.2f}".format(COMPOUND)
COMPOUND
```

### Calculate daily variations


```python
df_yahoo = df_yahoo.sort_values("Date", ascending=False).reset_index(drop=True)
```

#### Data now


```python
DATA_NOW = df_yahoo.loc[0, "Close"]
DATA_NOW
```

#### Data yesterday


```python
DATA_YESTERDAY = df_yahoo.loc[1, "Close"]
DATA_YESTERDAY
```

#### Calculate daily variations


```python
VARV = DATA_NOW - DATA_YESTERDAY
VARV = "{:+,.2f}".format(VARV)
VARV
```


```python
VARP = ((DATA_NOW - DATA_YESTERDAY) / DATA_NOW)*100
VARP = "{:+,.2f}".format(VARP)
VARP
```

#### Display current values


```python
DATA_NOW = round(DATA_NOW, 1)
DATA_NOW = "${:,.2f}".format(DATA_NOW)
DATA_NOW
```


```python
DATA_YESTERDAY = round(DATA_YESTERDAY, 1)
DATA_YESTERDAY = "${:,.2f}".format(DATA_YESTERDAY)
DATA_YESTERDAY
```

## Output

### Save chart as png and html


```python
chart.write_html(f"{ticker}.html")
chart.write_image(f"{ticker}.png", width=1200)
```

### Expose chart


```python
link_image = naas.asset.add(f"{ticker}.png")
link_html = naas.asset.add(f"{ticker}.html", {"inline":True})
```

### Create markdown template 


```python
%%writefile message.md
Hey <!here>

The *TICKER* price is *DATA_NOW* right now, VARV vs yesterday (VARP%).
Yesterday close : DATA_YESTERDAY

In +20 days, basic ML models predict the following prices: 

- *arima*: ARIMA
- *svr*: SVR
- *linear*: LINEAR
- *compound*: COMPOUND

<link_html |Open dynamic chart>
```


```python
markdown_file = "message.md"
md = open(markdown_file, "r").read()
md
```

### Replace values in template


```python
post = md.replace("DATA_NOW", str(DATA_NOW))
post = post.replace("TICKER", str(ticker))
post = post.replace("DATA_YESTERDAY", str(DATA_YESTERDAY))
post = post.replace("VARV", str(VARV))
post = post.replace("VARP", str(VARP))
post = post.replace("LINEAR", str(LINEAR))
post = post.replace("SVR", str(SVR))
post = post.replace("COMPOUND", str(COMPOUND))
post = post.replace("ARIMA", str(ARIMA))
post = post.replace("link_html", str(link_html))
post
```

### Post on Slack 


```python
message = post
image = link_image
slack.connect(token).send(channel, post, link_image)
```

### Add email template as a dependency


```python
## add as a dependency
naas.dependency.add("message.md")
```

### Schedule every day


```python
naas.scheduler.add(cron="0 9 * * *")

#naas.scheduler.delete() #if you want to delete the scheduler
```
