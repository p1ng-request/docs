<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Send_notifications_from_Google_Sheets.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Send+notifications+from+Google+Sheets:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #productivity #gsheet #naas_drivers #operations #snippet #email

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook allows users to send emails from a Google Sheets spreadsheet.

## Input

### Import libraries


```python
import naas_drivers
from naas_drivers import gsheet, emailbuilder, naasauth
import naas
```

### Setup Variables
Share your Google Sheets spreadsheet with our service account : 🔗 naas-share@naas-gsheets.iam.gserviceaccount.com
- `spreadsheet_url`: This variable stores the URL of a spreadsheet.
- `sheet_name`: This variable represents the name of a specific sheet within the spreadsheet.
- `first_name_col`: This variable stores the name or identifier of a column in the spreadsheet. 
- `email_col`: This variable represents the name or identifier of another column in the spreadsheet.
- `email_subject`: This variable stores the email subject.


```python
spreadsheet_url = "1swGTMX6d_N8-AVRueBEd8C0J6OlvO218iDSVMootWZk"
sheet_name = "Sheet1"
first_name_col = "FIRST NAME"
email_col = "EMAIL"
email_subject = "Merry Christmas & spread love for 2021 ❤️"
```

## Model

### Get data from Google Sheets spreadsheet


```python
df = naas_drivers.gsheet.connect(spreadsheet_url).get(sheet_name=sheet_name)
print("Row fechted:", len(df))
df.head(1)
```

### Mail preview


```python
email_content = naas_drivers.emailbuilder.generate(
    display="iframe",
    title="🎅 Merry Christmas",
    heading= emailbuilder.heading("& Happy new year {first_name} 🍾", text_align="center"),
    text_1=emailbuilder.text("Even if 2020 has been extremely difficult year, let's make 2021 better!"),
    text_2=emailbuilder.text("Keep smiling,"),
    text_3=emailbuilder.text("Keep laughing,"),
    text_4=emailbuilder.text("Spread love ❤️"),
)
```

## Output

### Sending emails


```python
firstname_list = data[first_name_col]
email_list = data[email_col]

for i in range(len(data)):
    content = email_content.replace("{first_name}", firstname_list[i])
    naas.notifications.send(
        email_to=email_list[i],
        subject=email_subject,
        html=content,
        email_from=naasauth.connect().user.me().get("username")
    )
```
