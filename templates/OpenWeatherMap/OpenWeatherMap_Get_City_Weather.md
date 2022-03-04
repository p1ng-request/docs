# OpenWeatherMap - Get City Weather
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenWeatherMap/OpenWeatherMap_Get_City_Weather.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #openweathermap #opendata

## Input

### Import library


```python
import requests
```

### Variables


```python
OPENWEATHER_KEY = '**********'  # get your key from here https://home.openweathermap.org/api_keys (it takes couples of minutes)
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
