# YahooFinance - Send daily prediction to Email
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/YahooFinance/YahooFinance_Send_daily_prediction_to_Email.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #yahoofinance #trading #markdown #prediction #plotly #slack #naas_drivers #scheduler #notification #asset #webhook #dependency #naas

With this template, you can create daily email prediction bot on any ticker available in [Yahoo finance](https://finance.yahoo.com/quote/TSLA/).<br> 

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/j%C3%A9r%C3%A9my-ravenel-8a396910/)

## Input

### Import libraries


```python
import naas
from naas_drivers import prediction, yahoofinance, plotly, slack
import markdown2
```

### Input ticker and dates
👉 Here you can change the ticker and timeframe


```python
ticker = "TSLA"
date_from = -100 # 1OO days max to feed the naas_driver for prediction
date_to = "today"
data_point = 20

# Output paths image and html
output_image = f"{ticker}.png"
output_html = f"{ticker}.html"
```

### Input email parameters
👉 Here you can input your sender email and destination email 

Note: emails are sent from notification@naass.ai by default


```python
email_to = ["template@naas.ai"]
email_from = None
```

## Model

### Get dataset from Yahoo Finance


```python
df_yahoo = yahoofinance.get(ticker, date_from=date_from, date_to=date_to)

# clean df
df_yahoo = df_yahoo.dropna()
df_yahoo.reset_index(drop=True)
df_yahoo.head()
```

### Add prediction columns


```python
df_predict = prediction.get(dataset=df_yahoo,
                            date_column='Date',
                            column="Close",
                            data_points=data_point,
                            prediction_type="all")
```


```python
df_predict = df_predict.sort_values("Date", ascending=False).reset_index(drop=True)
df_predict.head(30)
```

### Build chart


```python
chart = plotly.linechart(df_predict,
                         x="Date",
                         y=["Close", "ARIMA", "SVR", "LINEAR", "COMPOUND"],
                         showlegend=True,
                         title=f"{ticker} predictions as of today, for next {data_point} days.")
```

### Set daily variations values


```python
df_yahoo = df_yahoo.sort_values("Date", ascending=False).reset_index(drop=True)
```


```python
DATANOW = df_yahoo.loc[0, "Close"]
DATANOW
```


```python
DATAYESTERDAY = df_yahoo.loc[1, "Close"]
DATAYESTERDAY
```


```python
VARV = DATANOW - DATAYESTERDAY
VARV = "{:+,.2f}".format(VARV)
VARV
```


```python
VARP = ((DATANOW - DATAYESTERDAY) / DATANOW)*100
VARP = "{:+,.2f}".format(VARP)
VARP
```

### Format values


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


```python
DATANOW = round(DATANOW, 1)
DATANOW = "${:,.2f}".format(DATANOW)
DATANOW
```


```python
DATAYESTERDAY = round(DATAYESTERDAY, 1)
DATAYESTERDAY = "${:,.2f}".format(DATAYESTERDAY)
DATAYESTERDAY
```

## Output

### Save data in Excel


```python
df_predict.to_excel(f"{ticker}_TODAY.xlsx")
```

### Save chart in png and html


```python
chart.write_image(output_image, width=1200)
chart.write_html(output_html)
```

### Expose chart


```python
link_image = naas.asset.add(output_image)
link_html = naas.asset.add(output_html, {"inline":True})
```

### Add webhook to run your notebook again


```python
link_webhook = naas.webhook.add()
```

### Create markdown template 


```python
%%writefile message.md
Hello world,

The **TICKER** price is **DATANOW** right now, VARV vs yesterday (VARP%).<br>
Yesterday close : DATAYESTERDAY

In +20 days, basic ML models predict the following prices: 

- **arima**: ARIMA
- **svr**: SVR
- **linear**: LINEAR
- **compound**: COMPOUND
    
<img href=link_html target="_blank" src=link_image style="width:640px; height:360px;" /><br>
[Open dynamic chart](link_html)<br>

Please find attached the data in Excel.<br>

Have a nice day.
<br>

PS: You can [send the email again](link_webhook) if you need a fresh update.<br>
<div><strong>Full Name</strong></div>
<div>Open source lover | <a href="http://www.naas.ai/" target="_blank">Naas</a></div>
<div>+ 33 1 23 45 67 89</div>
<div><small>This is an automated email from my Naas account</small></div>
```


```python
markdown_file = "message.md"
content = open(markdown_file, "r").read()
md = markdown2.markdown(content)
md
```

### Replace values in template


```python
post = md.replace("DATANOW", str(DATANOW))
post = post.replace("TICKER", str(ticker))
post = post.replace("DATAYESTERDAY", str(DATAYESTERDAY))
post = post.replace("VARV", str(VARV))
post = post.replace("VARP", str(VARP))
post = post.replace("LINEAR", str(LINEAR))
post = post.replace("SVR", str(SVR))
post = post.replace("COMPOUND", str(COMPOUND))
post = post.replace("ARIMA", str(ARIMA))
post = post.replace("link_image", str(link_image))
post = post.replace("link_html", str(link_html))
post = post.replace("link_webhook", str(link_webhook))
post
```

### Send by Email


```python
subject = f"📈 {ticker} predictions as of today"
content = post
files = [f"{ticker}_TODAY.xlsx"]

naas.notification.send(email_to=email_to,
                       subject=subject,
                       html=content,
                       files=files,
                       email_from=email_from)
```

### Add email template as a dependency


```python
naas.dependency.add("message.md")
```

### Schedule every day


```python
naas.scheduler.add(cron="0 9 * * *")

# naas.scheduler.delete() #if you want to delete the scheduler
```
