<img width="10%" alt="Naas" src="https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160"/>

# Streamlit - Create prediction app
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Streamlit/Streamlit_Create_prediction_app.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #streamlit #app #ml

## Input

Create the Python file necessary to deploy Streamlit app.


```python
%%writefile streamlit_app.py

import streamlit as st
from naas_drivers.input.prediction import Prediction
from naas_drivers.input.yahoofinance import Yahoofinance
from naas_drivers.input.plotly import Plotly
yf = Yahoofinance()
pre = Prediction()
plotly = Plotly()

stock = "TSLA"

dataset = yf.get(stock_companies = stock)
pr = pre.get(dataset=dataset)
plt=plotly.stock(pr,"linechart_close")


st.write("# Prediction for {}".format(stock))
st.plotly_chart(plt)
```

### Import library


```python
from naas_drivers import streamlit
```

## Model & Output

### Deploy the app from Python file and serve the URL where the app is exposed (NgrokTunnel)


```python
streamlit.add("streamlit_app.py",port=9999, debug=False)
```
