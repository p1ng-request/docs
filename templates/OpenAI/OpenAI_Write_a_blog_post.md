<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Write_a_blog_post.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Write+a+blog+post:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #openai #blogpost #writing #ai #machinelearning #deeplearning

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will provide a step-by-step guide to writing a blog post using OpenAI.

**References:**
- [OpenAI Documentation](https://openai.com/docs/)
- [Writing a Blog Post](https://www.wikihow.com/Write-a-Blog-Post)

## Input

### Import libraries


```python
try:
    import openai
except:
    !pip install openai --user
    import openai
import naas
```

### Setup Variables
- `api_key`: OpenAI API key, to obtain an OpenAI API key, please refer to the [OpenAI Documentation](https://openai.com/docs/).
- `topic`: the topic of the blog post
- `tone`: the tone of the blog post
- `characters`: the number of characters of the blog post


<u>About "tone"</u>

Here are some different tones you can use for a blog post:
- Formal: Use proper language, professional terms, and formal sentence structures. This tone is best used for academic or business-related blog posts.
- Informative: Stick to facts and provide helpful information. Avoid adding your opinion and present the content in a straightforward and objective manner.
- Conversational: Write as if you're talking to a friend. Use casual language, contractions, and personal anecdotes. This tone is best suited for lifestyle or personal blogs.
- Inspirational: Write in a way that motivates and encourages readers. Use positive language, inspiring stories, and uplifting messages.
- Humorous: Add some humor and make readers laugh. Use witty remarks, funny anecdotes, and sarcastic comments to engage readers.
- Persuasive: Try to persuade readers to take action or change their mind about a topic. Use strong arguments, statistics, and emotional appeals to convince readers.
- Opinionated: Share your personal opinion on a topic. Use strong language, personal experiences, and bold statements to express your views.
- Educational: Teach readers something new. Use step-by-step instructions, infographics, and helpful tips to educate readers on a topic.
- Critical: Analyze a topic critically and provide a detailed analysis. Use logic, reasoning, and evidence to support your arguments.
- Empathetic: Write in a way that connects with readers on an emotional level. Use empathy, compassion, and understanding to create a sense of community and support.


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
topic = "OpenAI and chatGPT"
tone = "Informative"
characters = 1000
prompt = f"Write a {characters} characters blog post about {topic} with a {tone} tone and a catchy headline"

# Outputs
file_path = f"Blog_Post_{topic.replace(' ', '_')}_{tone}_{characters}_characters.txt"
```

## Model

### Send requests to OpenAI API


```python
openai.api_key = api_key
response = openai.Completion.create(
    engine="text-davinci-003",
    prompt=prompt,
    max_tokens=2084,
    temperature=0.7,
    top_p=0.9
)
```

### Get text


```python
text = response['choices'][0]['text']
print(text)
```

## Output

### Save text to txt file


```python
text_file = open(file_path, "w")
text_file.write(text)
text_file.close()
```
