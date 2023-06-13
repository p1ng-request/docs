<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenWeatherMap/OpenWeatherMap_Get_City_Weather.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenWeatherMap+-+Get+City+Weather:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openweathermap #opendata #snippet #dataframe

**Author:** [Christophe Blefari](https://www.linkedin.com/in/christopheblefari/)

**Description:** This notebook provides an easy way to access current weather data for any city using the OpenWeatherMap API.

## Input

### Import library


```python
import requests
```

### Variables


```python
OPENWEATHER_KEY = "**********"  # get your key from here https://home.openweathermap.org/api_keys (it takes couples of minutes)
CITY = "Paris"
```

## Model

### Fonctions


```python
def get_weather_info(city):
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={OPENWEATHER_KEY}"
    response = requests.get(url)
    return response.json()


def format_weather_data(data):
    return {
        "temp": f'{round(int(data["main"]["temp"]) - 273.15, 1)}°',
        "city": data["name"],
    }


def run(city):
    data = get_weather_info(city)
    return format_weather_data(data)
```

## Output

### Display result


```python
run(CITY)
```
