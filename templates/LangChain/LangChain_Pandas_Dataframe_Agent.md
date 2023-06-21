<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LangChain/LangChain_Pandas_Dataframe_Agent.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LangChain+-+Pandas+Dataframe+Agent:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #langchain #pandas #dataframe #agent #python #toolkit

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook shows how to use agents to interact with a pandas dataframe. It is mostly optimized for question answering.

**References:**
- [LangChain - Pandas Dataframe Agent](https://python.langchain.com/en/latest/modules/agents/toolkits/examples/pandas.html)

## Input

### Import libraries
Note: You may need to restart the kernel to use updated packages.


```python
try:
    import langchain
except:
    !pip install langchain tabulate typing-inspect==0.8.0 typing_extensions==4.5.0 --user
from langchain.agents import create_pandas_dataframe_agent
from langchain.llms import OpenAI
import pandas as pd
import naas
```

### Setup Variables
- `api_key`: OpenAI API key. [Get your API key here](https://openai.com/docs/api-overview/).
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output.
- `df`: pandas dataframe
- `question`: question to be asked to agent


```python
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
temperature = 0
df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]})
question = "what is the sum of column B?"
```

## Model

### Create Agent


```python
# Create Agent
agent = create_pandas_dataframe_agent(OpenAI(temperature=temperature, openai_api_key=api_key), [df], verbose=True)
```

## Output

### Display result


```python
res = agent.run(question)
print("Result:", res)
```

 
