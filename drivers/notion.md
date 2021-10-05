---
description: Interact with your Notion workspace.
---

# Notion

{% hint style="warning" %}
This driver is in beta. Contact us on [Slack](https://join.slack.com/t/naas-club/shared_invite/zt-r187or6p-CwaKutBTxVeIIw6zJ0DHkw) to use it.
{% endhint %}

If you are not familiar with Notion, check out their website. It's pretty amazing all-in-workspace.

Find below is their website👇

{% embed url="https://www.notion.so/login" caption="Login link" %}

Before anything, you have to connect to your account in Notion, create your integration and make sure it has access to your page or your database.

#### Step 1: Create an integration.

* Go to [https://www.notion.com/my-integrations](https://www.notion.com/my-integrations).
* Click the "+ New integration" button.
* Give your integration a name - I chose "Vacation Planner".
* Select the workspace where you want to install this integration.
* Click "Submit" to create the integration.
* Copy the "Internal Integration Token" on the next page and save it somewhere secure, e.g. a password manager.

![](https://files.readme.io/2ec137d-093ad49-create-integration.gif)



#### Step 2: Share a database with your integration

Integrations don't have access to any pages \(or databases\) in the workspace at first. **A user must share specific pages with an integration in order for those pages to be accessed using the API.** This helps keep you and your team's information in Notion secure.

Start from a new or existing page in your workspace. Insert a new database by typing `/table` and selecting a full page table. Give it a title. I've called mine "Weekend getaway destinations". Click on the `Share` button and use the selector to find your integration by its name, then click `Invite`.

![](https://files.readme.io/0a267dd-share-database-with-integration.gif)

## Connect

```python
from naas_drivers import notion 

token = "*********" 
notion.connect(token)
```

## Get database

```python
from naas_drivers import notion 

token = "*********"
database_url = "https://www.notion.so/naas-official/8910d64de001479c8494fbecbf52b525?v=4911d8baa8a5494a86f6215a6b0c95fe"
database = notion.connect(token).database.get(database_url)
database
```

## Create a blank page inside a database

```python
from naas_drivers import notion 

token = "*********"
database_url = "https://www.notion.so/naas-official/8910d64de001479c8494fbecbf52b525?v=4911d8baa8a5494a86f6215a6b0c95fe"

page = notion.connect(token).page.create(parent=database_url, title="Page title")
page
```

## Update a page inside a database with properties

```python
from naas_drivers import notion 

token = "*********"
page_url = "https://www.notion.so/naas-official/Daily-meeting-04-10-2021-2187d1d0f228491c8ef32de65dea8b1c"

page = notion.connect(token).page.get(page_url)

page.properties.title("Name","Page title")
page.properties.rich_text("Text","Ceci est toto")
page.properties.number("Number", 42)
page.properties.select("Select",["Value1","Value2","Value3"])
page.properties.multi_select("Muti Select",["Value1","Value2","Value3"])
page.properties.date("Date","2021-10-03T17:01:26") #Follow ISO 8601 format
page.properties.people("People", ["d40e767c-d7af-4b18-a86d-55c61f1e39a4"]) #list of ID of users
page.properties.checkbox("Checkbox", [("Validated",True), ("Connected",False)])
page.properties.url("URL","www.naas.ai")
page.properties.email("Email","jeremy@naas.ai")
page.properties.phone_number("Phone number","+33 6 21 83 11 12")

page.update()


#Not yet supported
#page.properties.formula()
#page.properties.relation()
#page.properties.rollup()
#page.properties.files()
```

## Create Block inside a page

The order in parathesis will define the order of the block creation. 

Each creation will be pushed at the end of the current page content.

```python
from naas_drivers import notion 

token = "*********"
page_url = "https://www.notion.so/naas-official/Daily-meeting-04-10-2021-2187d1d0f228491c8ef32de65dea8b1c"

page = notion.connect(token).page.get(page_url)

page.block.add.heading_1("Page title")
page.block.add.heading_2("Page title")
page.block.add.heading_3("Page title")
page.block.add.paragraph("Page title")
page.block.add.paragraph("Page that you do")
page.block.add.numbered_list_item()
page.block.add.to_do()
page.block.add.toggle()
page.block.add.child_page()
page.block.add.child_database()
page.block.add.embed()
page.block.add.to_do()
page.block.add.image()
page.block.add.video()
page.block.add.pdf()
page.block.add.bookmark()

#The order in parathesis will define the order of the block creation. 
page.update()
```

## Get the list of users

```python
from naas_drivers import notion 

token = "*********"

users = notion.connect(token).users.list()
users
```

Discover more usage of the API with Notion official documentation:

{% embed url="https://developers.notion.com/reference/intro" %}



