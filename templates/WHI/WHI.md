# WHI - 
<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WHI/WHI.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #whi #indicators #opendata #worldsituationroom

## Input

### Import libraries


```python
import pandas as pd
import naas
import os
from PIL import Image, ImageDraw, ImageFont
from datetime import date
```

## Model

### Get the name of the files present in output


```python
weights = {}
for filename in os.listdir('output/'):
    if filename != '.ipynb_checkpoints' :
        df = pd.read_csv(f'output/{filename}')
        weights[df['INDICATOR'].values[0]] = 1
```


```python
weights
```

### Change the weights of those files


```python
weights = {'COVID-19 Active Cases': 4, 
           'Sea Level': 2,
           'Delta global temperature': 4,
           'Arctic Sea Ice level (million square km)': 2
          }
```


```python
weights
```


```python
df = None
for filename in os.listdir('output/'):
    if filename != '.ipynb_checkpoints' :
        if df is not None:
            row = pd.read_csv(f'output/{filename}')
            ind = row['INDICATOR'].values[0]
            row['WEIGHT'] = weights[ind]
            df = df.append(row)
        else:
            df = pd.read_csv(f'output/{filename}')
            ind = df['INDICATOR'].values[0]
            df['WEIGHT'] = weights[ind]
```

## Output

### Weighted Average to create WHI


```python
df
```


```python
def whi(df):
    return round((df['VALUE']*df['WEIGHT']).sum() / df['WEIGHT'].sum(), 2)
def createOutput(value, datetime):
    img = Image.open("layout.png")
    d = ImageDraw.Draw(img)
    
    font = ImageFont.truetype('ArchivoBlack-Regular.ttf', 90)
    fill = (255,255,255)
    
    d.text((50,900), "{indicator}/10, {date}".format(date=datetime.strftime("%d/%m/%Y"), indicator=value), font=font, fill=fill)

    return img
```

### Display image


```python
img = createOutput(f'{whi(df)}' , date.today())
display(img)
```
