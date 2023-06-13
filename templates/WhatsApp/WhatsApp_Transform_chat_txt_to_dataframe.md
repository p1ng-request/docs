<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/WhatsApp/WhatsApp_Transform_chat_txt_to_dataframe.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=WhatsApp+-+Transform+chat+txt+to+dataframe:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #python #pandas #regex #whatsapp #chats


**Author:** [Mohit Singh](https://www.linkedin.com/in/mohwits/)

**Description:** This notebook transforms your WhatsApp chat export from txt to a dataframe.

## Input

### Import libraries


```python
import re
import pandas as pd
```

### Setup Variables

**Export chat history**

You can use the export chat feature to export a copy of the chat history from an individual or group chat.
1. Open the individual or group chat.
2. Tap > More > Export chat.
3. Choose to export without media.
4. Save it to your drive or choose your preferred option.

- `file_path`: file path of your chat in txt
- `group_chat_name`: enter group chat name if it's a group chat.


```python
file_path = "Chat WhatsApp with +00 0 00 00 00 00.txt"
group_chat_name = None
```

## Model

### Open chat file


```python
chat_txt =  open(file_path, 'r', encoding='utf-8')
chat_txt = chat_txt.read()
# print(chat_txt)
```

### Create dataframe from txt


```python
def create_dataframe(file, group_chat_name=None):
    # Regex pattern to separate date and time
    pattern = '\d{1,2}/\d{1,2}/\d{2,4},\s\d{1,2}:\d{2}\s-\s'
    
    # Splitting message and dates
    messages = re.split(pattern, file)[1:]
    dates = re.findall(pattern, file)
    
    # Create dataframe
    df = pd.DataFrame({'Message': messages, 'Date': dates, 'Group Chart': group_chat_name})
    
    # Convert messages_data type
    df['Date'] = pd.to_datetime(df['Date'], format='%d/%m/%Y, %H:%M - ')

    # List for user
    users = []
    # List for messages
    messages = []

    # Iterating in messages
    for message in df['Message']:
      # Splitting message with ':'
      entry = re.split('([\w\W]+?):\s', message)

      # If it has value after ':'
      if entry[1:]:
            users.append(entry[1])
            messages.append(entry[2][:-1])
      # If it does not have a user name
      else:
          # appending name as 'Notification'
          users.append('Notification')
          # appending message
          messages.append(entry[0][:-1])

    # Dropping previous message column
    df.drop('Message', axis = 1, inplace=True)

    # Adding user column with user names
    df['User'] = users
    # Adding message column with just message
    df['Message'] = messages

    # Separating Year, month, day, hour and minute from Date and creating specific column
    df['Year'] = df['Date'].dt.year
    df['Month'] = df['Date'].dt.month_name()
    df['Day'] = df['Date'].dt.day
    df['Hour'] = df['Date'].dt.hour
    df['Minute'] = df['Date'].dt.minute
    return df
```

## Output

### Display dataframe


```python
df_whatsapp = create_dataframe(chat_txt, group_chat_name)
print("Messages fetched:", len(df_whatsapp))
df_whatsapp
```
