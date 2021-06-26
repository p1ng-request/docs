---
description: Predict the time series data
---

# Prediction

Give a data frame with these columns

| Date | Close |
| :--- | :--- |
| 2014-04-14 | 133.95 |

Base data can come from Yahoo driver

## All

_**The model will predict SVR, LINEAR, ARIMA for 20 days on Close value**_

```python
dataset = naas_drivers.yahoo.stock("TSLA")
pr = naas_drivers.prediction.get(dataset=dataset, prediction_type="all")
```

## Prediction size

* `data_points`:  _**The number of days in the future that are to predict.**_

```python
dataset = naas_drivers.yahoo.stock("TSLA")
pr = naas_drivers.prediction.get(dataset=dataset, data_points=50)
```

## Model

> All the parameters of the above formula are explained below.

* `prediction_type`:  _**The model to predict, it can be SVR, LINEAR, ARIMA, or all**_

```text
dataset = naas_drivers.yahoo.stock("TSLA")
pr = naas_drivers.prediction.get(dataset=dataset, prediction_type="ARIMA")
```

## Options

* `dataset` : the dataset in DataFrame format
* `column`: The exact name of the column that is to be predicted, from the dataset
* `date_column`:The date range from the dataset. Will be used as the output index.
* `prediction_type`: _Can be ARIMA,_ LINEAR, SVR, COMPOUND or all
* `data_points` **\*\*\(optional\)**:\*\* number of days to predict
* `concact_label` \(optional\): A column name who will generate a concatenated frame with past and future data.

```python
dataset = naas_drivers.yahoo.stock("TSLA")
pr = naas_drivers.prediction.get(dataset=dataset)
```

## Plot

> Once you have predicted using the above predict formula, you can plot the predictions

```python
  naas_drivers.plotly.stock(pr, , "linechart_close")
```

Check more options on the link below

