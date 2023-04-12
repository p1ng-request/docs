<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Generate_Dialogue.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Generate+Dialogue:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #gpt #api #prompt

**Author:** [Sriniketh Jayasendil](https://www.linkedin.com/in/sriniketh-jayasendil/)

**Description:** This template shows how to use the OpenAI API to generate responses to user input within a Naas notebook, allowing users to create interactive chatbots or dialogue systems.

## Input

### Import libraries


```python
import naas
try:
    import openai
except ModuleNotFoundError:
    !pip install --user openai
    import openai
```

### Setup Variables


```python
#inputs
openai.api_key = naas.secret.get(name="OPENAI_API_KEY")
choice = 1  # to ask every time if the user wants to continue the conversation(1) or not(0)

#outputs
messages = {}  # Logs the prompts and response generated.
```

## Model

### Get the response from OpenAI API


```python
def gen_dialogue(prompt):
    response = openai.Completion.create(
      model="text-davinci-003",
      prompt=prompt,
      temperature=0.7,
      max_tokens=256,
      top_p=1.0,
      frequency_penalty=0.0,
      presence_penalty=0.0,
      stop=["\"\"\""]
    )
    
    print('\n🤖 OpenAI response: ' + response.choices[0].text)
    messages[prompt] = response.choices[0].text
```

## Output

### Store them in messages (dictionary) for logging the results


```python
while(choice):
    print()
    prompt = input('👤 Enter the prompt: ')
    gen_dialogue(prompt)
    print()
    choice = int(input('➡️ Enter the choice [0/1]: '))

print('\n\n\n')
print(messages)
```
