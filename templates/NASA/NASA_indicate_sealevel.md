```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
from datetime import date, datetime, timedelta
import math
from sktime.utils.plotting import plot_series
from sktime.forecasting.model_selection import (
    ExpandingWindowSplitter,
    ForecastingGridSearchCV,
    SlidingWindowSplitter,
    temporal_train_test_split,
)
from sktime.forecasting.arima import ARIMA, AutoARIMA
from sktime.forecasting.compose import (
    EnsembleForecaster,
    MultiplexForecaster,
    TransformedTargetForecaster,
    make_reduction,
)
import matplotlib.pyplot as plt
from sktime.forecasting.naive import NaiveForecaster
from sktime.forecasting.base import ForecastingHorizon
from sktime.performance_metrics.forecasting import (
    MeanAbsolutePercentageError,
    mean_absolute_percentage_error,
)
from scipy.interpolate import interp1d
from sklearn.neighbors import KNeighborsRegressor
import numpy as np
import os
import sys
import tempfile
import dateutil.parser
import matplotlib.dates as mdates
import naas
```


```python

```


```python
indicator = SeaLevelIndicator('nasa-sea-level-data.txt')
```


```python
'''
This is safer to use - it gives a value more inline with current projections, 
but can be reused with additional data
'''
indicator.value(method='curve_fit')
```


```python
df = indicator.value_df()
```


```python
naas.assets.add('nasa_sealevel_output.csv')
```


```python
df.to_csv('data_')
```


```python
indicator.value(method='arima')
```


```python
indicator.plot_projection(method='curve_fit')
```


```python
indicator.plot_projection(method='arima')
```

## Dataset
Source: Nasa (https://climate.nasa.gov/vital-signs/sea-level/)
URL: https://podaac-tools.jpl.nasa.gov/drive/files/allData/merged_alt/L2/TP_J1_OSTM/global_mean_sea_level/GMSL_TPJAOS_5.0_199209_202102.txt


```python
'''
Column descriptions
    1 altimeter type 0=dual-frequency  999=single frequency (ie Poseidon-1) 
    2 merged file cycle # 
    3 year+fraction of year (mid-cycle) 
    4 number of observations 
    5 number of weighted observations 
    6 GMSL (Global Isostatic Adjustment (GIA) not applied) variation (mm) with respect to 20-year 
        TOPEX/Jason collinear mean reference 
    7 standard deviation of GMSL (GIA not applied) variation estimate (mm)
    8 smoothed (60-day Gaussian type filter) GMSL (GIA not applied) variation (mm)  
    9 GMSL (Global Isostatic Adjustment (GIA) applied) variation (mm) with respect to 20-year 
        TOPEX/Jason collinear mean reference 
    10 standard deviation of GMSL (GIA applied) variation estimate (mm)
    11 smoothed (60-day Gaussian type filter) GMSL (GIA applied) variation (mm)
    12 smoothed (60-day Gaussian type filter) GMSL (GIA applied) variation (mm); 
      annual and semi-annual signal removed
Learn more @ https://sealevel.colorado.edu/presentation/what-definition-global-mean-sea-level-gmsl-and-its-rate
'''
pass
```

## Code


```python
class SeaLevelIndicator():
    def __init__(self, filepath):
        self.filepath = filepath
        self.df = self.get_df()
        
        
    def value_df(self, method='curve_fit'):
        value = self.value(method)
        data = {'DATE_PROCESSED': [datetime.today().date()],
                'INDICATOR': 'Sea Level',
                 'VALUE': [indicator.value()]}
        return pd.DataFrame.from_dict(data)
        
    def value(self, method='curve_fit'):
        # interpolate value out of ten
        m = (10-0)/(self.best_case(value_only=True)-self.worst_case(value_only=True))
        c = -self.worst_case(value_only=True) * m
        return m * self.current_projection(method=method, value_only=True) + c
    
    def current_projection(self, method='curve_fit', value_only=False):
        value = None
        if method.lower() == 'curve_fit':
            x = mdates.date2num(self.df_per_year['smoothed_GMSL_gia_signal_rem'].index)
            y = (self.df_per_year['smoothed_GMSL_gia_signal_rem'] \
                 + abs(self.df_per_year['smoothed_GMSL_gia_signal_rem'].min())).values
            z4 = np.polyfit(x, y, 3)
            p4 = np.poly1d(z4)
            xx = np.linspace(x.min(), mdates.date2num(datetime(2100, 12, 31)), 100)
            dd = mdates.num2date(xx)
            df = pd.DataFrame(data=p4(xx), index=dd) 
            value = df.iloc[-1].values[0]
        elif method.lower() == 'arima':
            df = self.df_starting_from_zero.copy()
            df = df.resample('M').mean()
            df.index = pd.PeriodIndex(df.index, freq="M")
            y_train, y_test = temporal_train_test_split(df['smoothed_GMSL_gia_signal_rem'],
                                                        test_size=180)
            future_months = (pd.Period('2100-12') - df['smoothed_GMSL_gia_signal_rem'].index[-1]).n
            forecaster = AutoARIMA(sp=12, suppress_warnings=True)
            alpha = 0.05  # 95% prediction intervals
            fh = np.arange(future_months) + 1 # forecast_horizon
            forecaster.fit(df['smoothed_GMSL_gia_signal_rem'])
            y_pred, pred_ints = forecaster.predict(fh, return_pred_int=True, alpha=alpha)
            value = y_pred.iloc[-1]
        if value_only:
            return value
        return {'date': 'December 2100',
                 'period': '2100-12',
                 'units': 'Sea Level above 2000 Levels (mm)',
                 'value': value}
            
    def best_case(self, value_only=False):
        # Source: https://tidesandcurrents.noaa.gov/publications/techrpt83_Global_and_Regional_SLR_Scenarios_for_the_US_final.pdf
        recorded_value = 300
        if value_only:
            return recorded_value
        return {'date': 'December 2100', 'period': '2100-12', 
                'units': 'Sea Level above 2000 Levels (mm)', 'value': recorded_value}
    
    def worst_case(self, value_only=False):
        # Source: https://tidesandcurrents.noaa.gov/publications/techrpt83_Global_and_Regional_SLR_Scenarios_for_the_US_final.pdf
        recorded_value = 2500
        if value_only:
            return recorded_value
        return {'date': 'December 2100', 'period': '2100-12', 
                'units': 'Sea Level above 2000 Levels (mm)', 'value': recorded_value}
    
    def plot_projection(self, method='curve_fit'):
        if method.lower() == 'curve_fit':
            x = mdates.date2num(self.df_per_year['smoothed_GMSL_gia_signal_rem'].index)
            y = (self.df_per_year['smoothed_GMSL_gia_signal_rem'] \
                 + abs(self.df_per_year['smoothed_GMSL_gia_signal_rem'].min())).values
            z4 = np.polyfit(x, y, 3)
            p4 = np.poly1d(z4)

            fig, cx = plt.subplots(figsize=(16, 4))

            xx = np.linspace(x.min(), mdates.date2num(datetime(2100, 12, 31)), 100)
            dd = mdates.num2date(xx)

            cx.plot(dd, p4(xx), '-g')
            cx.plot(x, y, '+', color='b', label='blub')
            cx.errorbar(x, y,
                         marker='.',
                         color='k',
                         ecolor='b',
                         markerfacecolor='b',
                         label="series 1",
                         capsize=0,
                         linestyle='')
            cx.grid()
            plt.show()
            
        elif method.lower() == 'arima':
            # Set the frequency of the index, Sktime needs this to work
            df = self.df_starting_from_zero.copy()
            df = df.resample('M').mean()
            df.index = pd.PeriodIndex(df.index, freq="M")
            y_train, y_test = temporal_train_test_split(df['smoothed_GMSL_gia_signal_rem'],
                                                        test_size=180)
            future_months = (pd.Period('2100-12') - df['smoothed_GMSL_gia_signal_rem'].index[-1]).n
            forecaster = AutoARIMA(sp=12, suppress_warnings=True)
            alpha = 0.05  # 95% prediction intervals
            fh = np.arange(future_months) + 1 # forecast_horizon
            forecaster.fit(df['smoothed_GMSL_gia_signal_rem'])
            y_pred, pred_ints = forecaster.predict(fh, return_pred_int=True, alpha=alpha)
            fig, ax = plot_series(df['smoothed_GMSL_gia_signal_rem'], 
                                  y_pred, labels=["y_train", "y_pred"])
            ax.fill_between(
                ax.get_lines()[-1].get_xdata(),
                pred_ints["lower"],
                pred_ints["upper"],
                alpha=0.2,
                color=ax.get_lines()[-1].get_c(),
                label=f"{1 - alpha}% prediction intervals",
            )
            ax.legend();
            
            
    def get_df(self):
        cols = ['altimeter_type','merged_file_cycle_#','yearfrac','num_obs','num_w_obs', 'GMSL_variation_mm',
        'std_GMSL','smoothed_GMSL','GMSL_GIA_variation_mm','std_GMSL_GIA','smoothed_gia_GMSL',
        'smoothed_GMSL_gia_signal_rem']
        with open(self.filepath, 'r') as f:
            data = f.read()
        data = [d[1:] for d in data.split('\n') if 'HDR' not in d]
        df = pd.DataFrame([l.split() for l in data], dtype=float, columns=cols)
        # Pre-processing        
        def convert_yearfrac_to_datetime(yearfrac):
            year = int(yearfrac)
            rem = yearfrac - year
            base = datetime(year, 1, 1)
            return base + timedelta(seconds=(base.replace(year=base.year + 1) - base).total_seconds() * rem)
        df['datetime'] = df['yearfrac'].apply(lambda year: convert_yearfrac_to_datetime(year))
        df = df[['datetime', 'smoothed_GMSL_gia_signal_rem']].set_index('datetime')
        return df
    
    def current_value(self, value_only=False):
        res = requests.get('https://climate.nasa.gov/vital-signs/sea-level/')
        soup = BeautifulSoup(res.text, 'html.parser')
        measurement = soup.find_all("div", {"class": "latest_measurement"})[0]
        date = measurement.find("span", {"class": "month_year"}).text.strip()
        value = measurement.find("div", {"class": "value"}).text.split('(')[0].strip()
        if value_only:
            return value
        try:
            period = dateutil.parser.parse(date).strftime('%Y-%m')
        except:
            period = None
        return {'date': date, 'period': period, 'current_value': value}
    
    @property
    def df_starting_from_zero(self):
        return self.df + abs(self.df.min()) # Here we add the minimum ensure measurements start at zero
    
    @property
    def df_per_year(self):
        return self.df.resample('Y').mean()
        
        
```


```python
# To Do 
# Neaten u notebook
# Test exponential upon adding datapoint
# Obtain indicator (based on exponential function)
# Try make notebook automatically updateable (retrieve data and clean automatically??)
# Make whatever-obtains-indicator a single function
# Package everything in a zip file and give to Jeremy
```

# NASA - Indicate sealevel
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/NASA/NASA_indicate_sealevel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

## Dataset
Source: Nasa (https://climate.nasa.gov/vital-signs/sea-level/)
URL: https://podaac-tools.jpl.nasa.gov/drive/files/allData/merged_alt/L2/TP_J1_OSTM/global_mean_sea_level/GMSL_TPJAOS_5.0_199209_202102.txt


```python
## Column descriptions ##
# 1 altimeter type 0=dual-frequency  999=single frequency (ie Poseidon-1) 
# 2 merged file cycle # 
# 3 year+fraction of year (mid-cycle) 
# 4 number of observations 
# 5 number of weighted observations 
# 6 GMSL (Global Isostatic Adjustment (GIA) not applied) variation (mm) with respect to 20-year 
#   TOPEX/Jason collinear mean reference 
# 7 standard deviation of GMSL (GIA not applied) variation estimate (mm)
# 8 smoothed (60-day Gaussian type filter) GMSL (GIA not applied) variation (mm)  
# 9 GMSL (Global Isostatic Adjustment (GIA) applied) variation (mm) with respect to 20-year 
#   TOPEX/Jason collinear mean reference 
# 10 standard deviation of GMSL (GIA applied) variation estimate (mm)
# 11 smoothed (60-day Gaussian type filter) GMSL (GIA applied) variation (mm)
# 12 smoothed (60-day Gaussian type filter) GMSL (GIA applied) variation (mm); 
#    annual and semi-annual signal removed

# Learn more @ https://sealevel.colorado.edu/presentation/what-definition-global-mean-sea-level-gmsl-and-its-rate
```

### 1. Get Current Value of Variable


```python
# 1.) Current sea height variation
def get_current_value():
    res = requests.get('https://climate.nasa.gov/vital-signs/sea-level/')
    soup = BeautifulSoup(res.text, 'html.parser')
    measurement = soup.find_all("div", {"class": "latest_measurement"})[0]
    date = measurement.find("span", {"class": "month_year"}).text.strip()
    value = measurement.find("div", {"class": "value"}).text.split('(')[0].strip()
    try:
        period = dateutil.parser.parse(date).strftime('%Y-%m')
    except:
        period = None
    return {'date': date, 'period': period, 'current_value': value}
current_value = get_current_value()
current_value
```


```python
dateutil.parser.parse('January 2021').strftime('%Y-%m')
```


```python
indicator.df_per_year
```


```python
# 2.) Change in mm per year
res = requests.get('https://climate.nasa.gov')
soup = BeautifulSoup(res.text, 'html.parser')
vital_containers = soup.find_all("div", {"class": "readout"})
def extract_vital(el):
    vital = {}
    vital['title'] = el.find("div", {"class": "title"}).text.strip()
    vital['units'] = el.find("div", {"class": "units"}).text.strip()
    temp = el.find("div", {"class": "change_number"}).text.strip()
    if isinstance(temp, str):
        vital['value'] = float(temp)
    else:
        vital['value'] = temp
    vital['description'] = el.find("div", {"class": "vital_signs_description"}).text.strip()
    return vital
vitals = [extract_vital(el) for el in vital_containers]
def specific_vital(title):
    for vital in vitals:
        if vital.get('title') == title:
            return vital
    return None
current_change_per_year = specific_vital('Sea Level')['value']
current_change_per_year
```


```python
specific_vital('Sea Level')
```

### 2. Get Current Projection of Variable



```python
df = pd.read_csv('nasa-wrangled.txt', skiprows=30)
df.head(2)
```


```python
def convert_yearfrac_to_datetime(yearfrac):
    year = int(yearfrac)
    rem = yearfrac - year
    base = datetime(year, 1, 1)
    return base + timedelta(seconds=(base.replace(year=base.year + 1) - base).total_seconds() * rem)
def sea_level(row):
    return row[['TOPEX/Poseidon', 'Jason-1', 'Jason-2', 'Jason-3']].mean()

df['datetime'] = df['yearfrac'].apply(lambda year: convert_yearfrac_to_datetime(year))
```


```python
columns = ['datetime', 'smoothed_GMSL_gia_signal_rem']
df = df[columns].set_index('datetime')
sea_height_variation = df + abs(df.min()) # Here we add the minimum ensure measurements start at zero
sea_height_variation_py = df.resample('Y').mean()
# df.resample('Y').mean().diff().plot()
```


```python

```


```python
sea_height_variation['smoothed_GMSL_gia_signal_rem'].plot(figsize=(16, 4))
```


```python
# Set the frequency of the index, Sktime needs this to work
sea_height_variation = sea_height_variation.resample('M').mean()
sea_height_variation.index = pd.PeriodIndex(sea_height_variation.index, freq="M")
y_train, y_test = temporal_train_test_split(sea_height_variation['smoothed_GMSL_gia_signal_rem'],
                                            test_size=180)
plot_series(y_train, y_test, labels=["y_train", "y_test"])
print(f'Training dataset size = {y_train.shape[0]} values, test dataset size = {y_test.shape[0]}')
```


```python
fh = np.arange(len(y_test)) + 1
```


```python
forecaster = AutoARIMA(sp=12, suppress_warnings=True)
alpha = 0.05  # 95% prediction intervals
```


```python
forecaster.fit(y_train)
y_pred, pred_ints = forecaster.predict(fh, return_pred_int=True, alpha=alpha)
error = mean_absolute_percentage_error(y_pred, y_test)
print(f'The mean absolute error is {error}')
```


```python
fig, ax = plot_series(y_train, y_test, y_pred, labels=["y_train", "y_test", "y_pred"])
ax.fill_between(
    ax.get_lines()[-1].get_xdata(),
    pred_ints["lower"],
    pred_ints["upper"],
    alpha=0.2,
    color=ax.get_lines()[-1].get_c(),
    label=f"{1 - alpha}% prediction intervals",
)
ax.legend();
```


```python
sea_height_variation
```


```python
future_months = (pd.Period('2100-12') - sea_height_variation['smoothed_GMSL_gia_signal_rem'].index[-1]).n
fh = np.arange(future_months) + 1
forecaster.fit(sea_height_variation['smoothed_GMSL_gia_signal_rem'])
y_pred, pred_ints = forecaster.predict(fh, return_pred_int=True, alpha=alpha)
fig, ax = plot_series(sea_height_variation['smoothed_GMSL_gia_signal_rem'], 
                      y_pred, labels=["y_train", "y_pred"])
ax.fill_between(
    ax.get_lines()[-1].get_xdata(),
    pred_ints["lower"],
    pred_ints["upper"],
    alpha=0.2,
    color=ax.get_lines()[-1].get_c(),
    label=f"{1 - alpha}% prediction intervals",
)
ax.legend();
```


```python
import scipy
import matplotlib.dates as mdates
```


```python
x = mdates.date2num(sea_height_variation_py['smoothed_GMSL_gia_signal_rem'].index)
y = (sea_height_variation_py['smoothed_GMSL_gia_signal_rem'] \
     + abs(sea_height_variation_py['smoothed_GMSL_gia_signal_rem'].min())).values
scipy.optimize.curve_fit(lambda t,a,b: a*np.exp(b*t), x , y)
```


```python
# x = np.append(x, 19592)
# y = np.append(y, 108)
```


```python
from matplotlib import pyplot as plt
z4 = np.polyfit(x, y, 3)
p4 = np.poly1d(z4)

fig, cx = plt.subplots(figsize=(16, 4))

xx = np.linspace(x.min(), mdates.date2num(datetime(2100, 12, 31)), 100)
dd = mdates.num2date(xx)

cx.plot(dd, p4(xx), '-g')
cx.plot(x, y, '+', color='b', label='blub')
cx.errorbar(x, y,
             marker='.',
             color='k',
             ecolor='b',
             markerfacecolor='b',
             label="series 1",
             capsize=0,
             linestyle='')

cx.grid()
plt.show()
```


```python
y
```


```python

```
