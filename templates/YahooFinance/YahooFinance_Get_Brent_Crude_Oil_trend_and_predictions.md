<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/YahooFinance/YahooFinance_Get_Brent_Crude_Oil_trend_and_predictions.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=YahooFinance+-+Get+Brent+Crude+Oil+trend+and+predictions:+Error+short+description">Bug report</a>

**Tags:** #commodities #energy #petrol #oil #yahoofinance #trading #markdown #prediction #plotly #naas_drivers #notification #naas #investors #automation #analytics #ai #html #image

**Author:** [Ayoub Berdeddouch](https://www.linkedin.com/in/ayoub-berdeddouch/)

With this template, you will access to a linechart chart that shows the Brend Crude Oil trend from [Yahoo finance](https://finance.yahoo.com/quote/TSLA/) for the past 9 months, and different algorithms predictions options for the next 3 months.<br> 
<u>Disclaimer:</u> The content of this notebook is not an investment advice and does not constitute any offer or solicitation to invest.

## Input

### Import libraries


```python
import naas
from naas_drivers import prediction, yahoofinance, plotly
import plotly.graph_objects as go
import markdown2
from datetime import datetime
from IPython.core.display import display, HTML
```

### Setup Yahoo Finance
👉 Here you can change the ticker and timeframe


```python
NAME = "Brend Crude Oil"
TICKER = "BZ=F"
date_from = -270
date_to = "today"
```

### Setup Prediction
👉 Here you can change the number of data points you want the prediction will be performed on


```python
DATA_POINT = 90
```

### Setup Assets


```python
NOW = datetime.now().strftime("%Y-%m-%d")
excel_output = f"{TICKER}_{NOW}.xlsx"
image_output = f"{TICKER}.png"
html_output = f"{TICKER}.html"
```

### Setup Naas scheduler
If you need to run this notebook on schedule, uncomment the first line of this cell.


```python
#naas.scheduler.add(cron="0 9 * * *")

# if you want to delete the scheduler, uncoment the line below and execute the cell
#naas.scheduler.delete() 
```

## Model

### Get dataset from Yahoo Finance


```python
df_yahoo = yahoofinance.get(tickers=TICKER,
                            date_from=date_from,
                            date_to=date_to).dropna().reset_index(drop=True)

# Display dataframe
df_yahoo.tail(5)
```

### Add prediction columns


```python
df_predict = prediction.get(dataset=df_yahoo,
                            date_column='Date',
                            column="Close",
                            data_points=DATA_POINT,
                            prediction_type="all").sort_values("Date", ascending=False).reset_index(drop=True)
# Display dataframe
df_predict.head(int(DATA_POINT)+5)
```

### Plot linechart


```python
fig = plotly.linechart(df_predict,
                       x="Date",
                       y=["Close", "ARIMA", "SVR", "LINEAR", "COMPOUND"],
                       showlegend=True,
                       title=f"{NAME} trend and predictions for the next {str(DATA_POINT)} days")
```

### Set actual data and variation


```python
def get_variation(df):
    df = df.sort_values("Date", ascending=False).reset_index(drop=True)
    
    # Get value and value comp
    datanow = df.loc[0, "Close"]
    datayesterday = df.loc[1, "Close"]
    
    # Calc variation en value and %
    varv = datanow - datayesterday
    varp = (varv / datanow)
    
    # Format result
    datanow = "${:,.2f}".format(round(datanow, 1))
    datayesterday = "${:,.2f}".format(round(datayesterday, 1))
    varv = "{:+,.2f}".format(varv)
    varp = "{:+,.2%}".format(varp)
    return datanow, datayesterday, varv, varp

DATANOW, DATAYESTERDAY, VARV, VARP = get_variation(df_yahoo)
print("Value today:", DATANOW)
print("Value yesterday:", DATAYESTERDAY)
print("Var. in value:", VARV)
print("Var. in %:", VARP)
```

### Set predict data


```python
def get_prediction(df, prediction):
    data = df.loc[0, prediction]
    
    # Format result
    data = "${:,.2f}".format(round(data, 1))
    return data

ARIMA = get_prediction(df_predict, "ARIMA")
print("Value ARIMA:", ARIMA)
SVR = get_prediction(df_predict, "SVR")
print("Value SVR:", SVR)
LINEAR = get_prediction(df_predict, "LINEAR")
print("Value LINEAR:", LINEAR)
COMPOUND = get_prediction(df_predict, "COMPOUND")
print("Value COMPOUND:", COMPOUND)
```

## Output

### Save and share the dataframe in Excel


```python
df_predict.to_excel(excel_output)
```

### Save and share your graph in PNG


```python
# Save your graph in PNG
fig.write_image(image_output)

# Share output with naas
link_image = naas.asset.add(image_output)

#-> Uncomment the line below to remove your asset
# naas.asset.delete(image_output)
```

### Save and share your graph in HTML



```python
# Save your graph in HTML
fig.write_html(html_output)

# Share output with naas
link_html = naas.asset.add(html_output, params={"inline": True})

#-> Uncomment the line below to remove your asset
# naas.asset.delete(html_output)
```
