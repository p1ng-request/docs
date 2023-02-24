<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/OpenAI/OpenAI_Write_a_social_media_post.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=OpenAI+-+Write+a+social+media+post:+Error+short+description">Bug report</a>

**Tags:** #openai #socialmedia #post #prompt #tone #platform

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will create a prompt to write a social media post and be able to set the topic, the tone and the platform.

**References:**
- [OpenAI](https://openai.com/)
- [Social Media Post](https://en.wikipedia.org/wiki/Social_media_post)

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
- `platform`: social media platform to publish your post on


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

<u>About "social media platforms"</u>

Here's a list of social media platforms where you can write articles:
- LinkedIn: LinkedIn is a professional social media platform where you can publish articles on industry-related topics. It's a great place to establish yourself as a thought leader and connect with other professionals in your field.
- Facebook Notes: Facebook Notes is a feature on Facebook that allows users to write long-form posts and publish them to their profile or page. It's a great way to share personal stories or thoughts with your friends and followers.
- Twitter Threads: Twitter Threads are a series of connected tweets that can be used to share longer thoughts or stories. It's a great way to break up longer articles into bite-sized pieces and share them with your Twitter followers.
- Instagram Stories: Instagram Stories are a feature on Instagram that allows users to share short videos or images that disappear after 24 hours. It can be a great way to share personal stories or behind-the-scenes glimpses into your life or business.
- Reddit: Reddit is a social news aggregation and discussion platform where users can post articles, stories, and links to other websites. It's a great platform for niche communities and can be a good place to share your writing with like-minded individuals.


```python
# Inputs
api_key = naas.secret.get(name="OPENAI_API_KEY") or "ENTER_YOUR_OPENAI_API_KEY"
topic = "The benefits of meditation"
tone = "Provocative"
platform = "Twitter"
prompt = f"Write a {tone.lower()} social media post about '{topic}' for {platform}."

# Outputs
file_path = f"Social_Media_Post_{topic.replace(' ', '_')}_{tone}_on_{platform}_characters.txt"
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

 
