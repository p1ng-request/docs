<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LangChain/LangChain_CSV_Agent.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=LangChain+-+CSV+Agent:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #csv #agent #langchain #questionanswering #toolkit #example

**Author:** [Hamid Mukhtar](https://www.linkedin.com/in/mukhtar-hamid/)

**Description:** This notebook shows how to use agents to interact with a csv. It is mostly optimized for question answering.

**References:**
- [LangChain - CSV Agent](https://python.langchain.com/docs/modules/agents/toolkits/csv)
- [LangChain - Agents](https://python.langchain.com/en/latest/modules/agents/index.html)

## Input

### Import libraries
Note: You may need to restart the kernel to use updated packages.


```python
try:
    import langchain
except:
    !pip install langchain tabulate typing-inspect==0.8.0 typing_extensions==4.5.0 --user
from langchain.agents import create_csv_agent
from langchain.llms import OpenAI
from langchain.chat_models import ChatOpenAI
from langchain.agents.agent_types import AgentType
import pandas as pd
import naas
```

### Setup Variables
- `api_key`: OpenAI API key. [Get your API key here](https://openai.com/docs/api-overview/).
- `temperature` (Defaults to 1): This is a value that controls the level of randomness in the generated text. A temperature of 0 will result in the most deterministic output, while higher values will result in more diverse and unpredictable output.
- `csv_path`: CSV path
- `question`: question to be asked to agent


```python
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
temperature = 0
csv_path = "https://covid.ourworldindata.org/data/owid-covid-data.csv"
question = "what is the number of total_cases in France?"
```

## Model

### Read CSV


```python
df = pd.read_csv(csv_path)
df.head(1)
```

### Create Agent


```python
# Create Agent
agent = create_csv_agent(
    OpenAI(temperature=temperature, openai_api_key=api_key),
    csv_path,
    verbose=True
)
```

## Output

### Display result


```python
res = agent.run(question)
print("Result:", res)
```

 
