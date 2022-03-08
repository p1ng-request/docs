<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/LinkedIn/LinkedIn%2BNotion_Update_metrics_in_content_calendar_from_posts.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a>

**Tags:** #linkedin #profile #post #feed #naas_drivers #notion #automation #analytics #naas #scheduler

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

With this notebook, you can update your content calendar in Notion with all metrics from your posts in LinkedIn:
- **Publication date:** When your post has been published.
- **Name:** First sentence of your post.
- **Content type:** Content type of you past post (Image, Text, Video, Article, Polls).
- **Platform:** "LinkedIn" by default.
- **Status:** "Published ✨" by default.
- **Engagment score:** Ratio between views and likes/comments
- **Views:** Amount of people who saw the content.
- **Likes:** Amount of people who pushed the like (or other reaction) button
- **Comments:** Amount of people who wrote something in the comment section.
- **Shares:** Amount of people who shared the content.
- **Profile mention:** People you mentioned.  
- **Company mention:** Companies you mentioned.
- **Nb Tags:** Number of hashtags.
- **Tags:** List of the hashtags.  
- **Nb emojis:** Number of emojis.
- **Emojis:** List of emojis.
- **Nb links:** Number of links.
- **Links:** Links used in your past posts.
- **Nb characters:** Number of characters in the past post.  
- **Content URL:** URL of the content 
- **Last refresh:** Date of last refresh in Notion

## Input

### Import libraries
Here below is the list of tools needed.


```python
import naas
from naas_drivers import linkedin, notion, emailbuilder, gsheet
from datetime import datetime
import pandas as pd
import plotly.express as px
import os
import requests
```

### Setup LinkedIn
<a href='https://www.notion.so/LinkedIn-driver-Get-your-cookies-d20a8e7e508e42af8a5b52e33f3dba75'>How to get your cookies ?</a>


```python
# Lindekin cookies
LI_AT = "AQEDARCNSioDe6wmAAABfqF-HR4AAAF-xYqhHlYAtSu7EZZEpFer0UZF-GLuz2DNSz4asOOyCRxPGFjenv37irMObYYgxxxxxxx"
JSESSIONID = "ajax:12XXXXXXXXXXXXXXXXX"

# Linkedin profile url
profile_url = "https://www.linkedin.com/in/xxxxxx/"
```

### Setup Notion
- Configure naas integration
- Duplicate <a href="https://naas-official.notion.site/724fec443b134f288b356001bb1543bd?v=c82a8005a5bf4862b7c967a9689aa799">content calendar template</a>
- Share integration on the template


```python
# Notion parameters
notion_token = "secret_eaLtxxxxxxxzuBPQvParsFxxxxxxx"
notion_database = 'https://www.notion.so/naas-official/fc64df2aae7f4796963d14edec816xxxxx'
```

### Setup your email
Please put your email so we get inform when your cookies need to renewed.


```python
# Email
EMAIL = "email"
```

### Schedule your notebook
This notebook can run on schedule. It will look for new data in LinkedIn and update accordingly to Notion.<br>
Note: You need to remove the hashtag and run cell to activate the scheduler.


```python
naas.scheduler.add(cron="0 8 * * *")

#-> To delete your scheduler, please uncomment the line below and execute this cell
# naas.scheduler.delete()
```

## Model

### Email sent to renew your cookies


```python
def email_linkedin_limit(email):
    content = {
       "header_naas": ("<a href='https://www.naas.ai/'>"
                       "<img align='center' width='30%' target='_blank' style='border-radius:5px;'"
                       "src='https://landen.imgix.net/jtci2pxwjczr/assets/5ice39g4.png?w=160'"
                       "alt='Please provide more information.'/>"
                       "</a>"),
        "txt_0": emailbuilder.text(f"Hi there,<br><br>"
                                   "Your LinkedIn cookies needs to be renewed.<br><br>"
                                   "Please go to naas and update them in your notebook 'Setup LinkedIn'.<br>"),
        "button": emailbuilder.button(f"https://app.naas.ai/user/{email}/", "Go to Naas"),
        "signature": "Naas Team",
        "footer": emailbuilder.footer_company(naas=True)
    }
    email_content = emailbuilder.generate(display='iframe', **content)
    return email_content

# email_content = email_linkedin_limit(EMAIL)
```

### Get content calendar from Notion
It will get all posts already created in Notion


```python
db_notion = notion.connect(notion_token).database.get(notion_database)
df_notion = db_notion.df()
print("📊 Post in Notion database:", len(df_notion))
```

### Get new posts in LinkedIn
It will get the new posts not created in Notion.


```python
# Get last post url in Notion
last_post_url = None
if len(df_notion) > 0:
    df_last_post = df_notion.sort_values(by="Publication Date", ascending=False).reset_index(drop=True)
    last_post_url = df_last_post.loc[0, "Content URL"]
    print("👉 Last post url:", last_post_url)
    
# Get new post created in LinkedIn
try:
    until = {}
    if last_post_url:
        until = {"POST_URL": last_post_url}
    df_posts_feed = linkedin.connect(LI_AT, JSESSIONID).profile.get_posts_feed(profile_url, until=until, limit=-1, sleep=False)
    df_posts_feed = df_posts_feed[df_posts_feed.POST_URL != last_post_url]
    print("🚀 New posts:", len(df_posts_feed))
except Exception as e:
    print("❌ Error")
    if e.response.status_code == 302:
        email_content = email_linkedin_limit(EMAIL)
        naas.notification.send(email_to=EMAIL,
                               subject="⚠️ naas.ai - Update your Linkedin cookies",
                               html=email_content)
        raise(e)
```

### Get stats from posts
It will get stats from all posts : Engagement Score, Views, Likes, Comments, Shares and Polls results


```python
# limit to last 50 posts
try:
    df_posts_stats = pd.DataFrame()
    count = 50
    limit = 50
    if len(df_notion) < 100:
        count = len(df_notion)
        limit = len(df_notion)
    if len(df_notion) > 0:
        df_posts_stats = linkedin.connect(LI_AT, JSESSIONID).profile.get_posts_feed(profile_url,
                                                                                    count=count,
                                                                                    limit=limit)
        print("🔄 Posts stats to update:", len(df_posts_stats))
except Exception as e:
    print("❌ Error")
    if e.response.status_code == 302:
        email_content = email_linkedin_limit(EMAIL)
        naas.notification.send(email_to=EMAIL,
                               subject="⚠️ naas.ai - Update your Linkedin cookies",
                               html=email_content)
        raise(e)
```

## Output


```python
def create_polls_graph(uid, title, data):
    # Create dataframe
    df = pd.melt(pd.DataFrame([data]))
    df = df.sort_values(by="value")
    voters = df.value.sum()
    
    # Create fig
    fig = px.bar(df,
                 y="variable",
                 x="value",
                 orientation='h',
                 title=f"{title}<br><span style='font-size: 13px;'>Total amount of votes: {voters}</span>",
                 text="value",
                 labels={"variable": "Poll options",
                         "value": "Poll results"}
                 )
    fig.update_traces(marker_color='black')
    fig.update_layout(
        plot_bgcolor="#ffffff",
        width=600,
        height=400,
        font=dict(family="Arial", size=14, color="black"),
        paper_bgcolor="white",
        xaxis_title=None,
        xaxis_showticklabels=False,
        yaxis_title=None,
        margin_pad=10,
    )
    fig.write_html(f"{uid}.html")
    asset = naas.asset.add(f"{uid}.html", params={"inline": True})
    return asset

def update_poll_graph(row):
    poll_graph = None
    
    # Add polls
    poll_id = row.POLL_ID
    poll_question = row.POLL_QUESTION
    poll_results = row.POLL_RESULTS
    if poll_id and poll_question and poll_results:
        poll_graph = create_polls_graph(poll_id, poll_question, poll_results)
    return poll_graph
```


```python
def update_dynamic_properties(page, row):
    # Page properties : dynamic
    page.number("Engagment score", float(row.ENGAGEMENT_SCORE))
    page.number("Views", int(row.VIEWS))
    page.number("Likes", int(row.LIKES))
    page.number("Comments", int(row.COMMENTS))
    page.number("Shares", int(row.SHARES))
    return page
```


```python
def update_content_notion(df, database_url):
    # Decode database id
    database_id = database_url.split("/")[-1].split("?v=")[0]
    
    # Get pages from notion database
    pages = notion.database.query(database_id, query={})
    
    # Manage dataframe empty
    if len(df) == 0:
        print(f"🛑 Nothing to update in Notion.")
        return
    
    # Loop in data
    df.COMPANY_MENTION = df.COMPANY_MENTION.fillna("")
    df.PROFILE_MENTION = df.PROFILE_MENTION.fillna("")
    for i, row in df.iterrows():
        title = row.TITLE
        content_title = row.CONTENT_TITLE
        if title is None and content_title is not None:
            title = f"Repost - {content_title}"
        elif title is None and content_title is None:
            title = "Repost"
        post_url = row.POST_URL
        print(post_url)
        
        # Create or update page
        page_new = True
        for page in pages:
            page_temp = page.df()
            page_id = page_temp.loc[page_temp.Name == "Content URL", "Value"].values
            if page_id == post_url:
                page_new = False
                break
        try:
            if page_new:
                # Create new page in notion
                page = notion.Page.new(database_id=database_id).create()

                # Page properties : static
                page.date("Publication Date", row.PUBLISHED_DATE)
                page.title("Name", title)
                page.select("Content type", row.CONTENT)
                page.select("Platform", "LinkedIn")
                page.select("Status", "Published ✨")
                profile_mention = row.COMPANY_MENTION
                if profile_mention is not None:
                    if len(profile_mention) > 2:
                        page.rich_text("Profile mention", profile_mention)
                company_mention = row.COMPANY_MENTION
                if company_mention is not None:
                    if len(company_mention) > 2:
                        page.rich_text("Company mention", company_mention)
                page.number("Nb tags", int(row.TAGS_COUNT))
                tags = row.TAGS
                if tags is None:
                    tags = ""
                else:
                    if len(tags) < 2:
                        tags = ""
                page.rich_text("Tags", tags)
                page.number("Nb emojis", int(row.EMOJIS_COUNT))
                emojis = row.EMOJIS
                if emojis is None:
                    emojis = ""
                else:
                    if len(emojis) < 2:
                        emojis = ""
                page.rich_text("Emojis", emojis)
                page.number("Nb links", int(row.LINKS_COUNT))
                links = row.LINKS
                if links is not None:
                    if len(links) > 2:
                        page.link("Links", links)
                page.number("Nb characters", int(row.CHARACTER_COUNT))
                page.link("Content URL", post_url)
                
                # Page blocks text
                page.heading_1("Text")
                text = row.TEXT
                if text is not None:
                    split_text = text.split("\n")
                    for t in split_text:
                        page.paragraph(t)
                    
                # Page blocks content
                image_url = row.IMAGE_URL
                content_url = row.CONTENT_URL
                poll_question = row.POLL_QUESTION
                if image_url or content_title or content_url or poll_question:
                    page.heading_1("Content")
                
                # Add image in content section
                if image_url:
                    page.heading_2("Image")
                    page.paragraph(image_url)
                    
                # Add post in content section
                if content_title:
                    page.heading_2("Media")
                    page.heading_3(content_title)
                
                if content_url:
                    page.paragraph(content_url)
                
                # Add poll graph in content section
                if poll_question:
                    page.heading_3("Poll")
                    poll_graph = update_poll_graph(row)
                    if poll_graph:
                        page.embed(poll_graph)
                
                # Page properties : dynamic
                page = update_dynamic_properties(page, row)
                
                # Create page in Notion
                page.update()
                print(f"✅ Page '{title}' created in Notion.", '\n')
            else:
                # Update poll graph
                update_poll_graph(row)
                
                # Page properties : dynamic
                page = update_dynamic_properties(page, row)
                
                # Update page
                page.update()
                print(f"📈 Post stats updated in notion for page '{title}'.", '\n')
        except Exception as e:
            print(f"❌ Error creating page '{title}' in Notion", e)
            print(row)
```

### Create new post page in Notion


```python
update_content_notion(df_posts_feed, notion_database)
```

### Update post stats in Notion


```python
update_content_notion(df_posts_stats, notion_database)
```

### Archive data in naas


```python
def archive_csv(df, profile_url=None, output_dir=None):
    if profile_url is not None:
        profile_id = profile_url.split("https://www.linkedin.com/in/")[-1].split("/")[0]
        filename=f"LINKEDIN_POSTS_FEED_{profile_id}.csv"
    else:
        filename="LINKEDIN_POSTS_FEED.csv"
    # Add timestamp to df
    df["DATE_EXTRACT"] = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    # Get archive
    df_archive = pd.DataFrame()
    files = os.listdir(output_dir)
    for f in files:
        if f == filename:
            df_archive = pd.read_csv(filename)
            break
            
    # Concat
    df = pd.concat([df, df_archive], axis=0)
    df.ACTIVITY_ID = df.ACTIVITY_ID.astype(str)
    df = df.drop_duplicates(subset=["ACTIVITY_ID"])
    df.to_csv(filename, index=False)
    return df
```


```python
df = archive_csv(df_posts_feed, profile_url)
print("💾 Linkedin posts archives:", len(df))
```
