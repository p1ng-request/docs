<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Python/Python_Get_random_word.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Python+-+Get+a+random+word:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #word #random #snippet 

**Author:** [Benjamin Filly](https://www.linkedin.com/in/benjamin-filly-05427727a/)

**Description:** This notebook show how to get a random word.

**References:**
- [The Natural Language Toolkit](https://pypi.org/project/nltk/)

## Input

### Import libraries


```python
import random
try:
    from nltk.corpus import wordnet
except:
    !pip install nltk --user
    from nltk.corpus import wordnet
import nltk
```

### Setup Variables
- `length`:  Length of the word you want to generate, if `length` is equal to 0 then there are no limits.


```python
length = 0
```

## Model

### Database installation

This line of code installs a database, for naas users it will be on `/home/ftp/`.


```python
nltk.download('wordnet')
```

### Get a random word


```python
def get_random_word(length):
    synsets = list(wordnet.all_synsets())
    if length <= 0:
        filtered_words = [synset.lemmas()[0].name() for synset in synsets]
    else:
        filtered_words = [synset.lemmas()[0].name() for synset in synsets if len(synset.lemmas()[0].name()) == length]

    if len(filtered_words) == 0:
        return None

    random_word = random.choice(filtered_words)
    return random_word
```

## Output

### Display result


```python
random_word = get_random_word(length)
if random_word:
    print("Random word found:", random_word)
else:
    print(f"No word of length {length} found.")
```
