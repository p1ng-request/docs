<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Get_time_entries_for_a_user_on_workspace.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Get+time+entries+for+a+user+on+workspace:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #timeentry #api #python #workspace #user

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will show how to get time entries for a user on a workspace using Clockify API. It will return a dataframe with columns as follow:
- id: This column stores an identifier or unique identifier associated with a time entry. It likely contains alphanumeric values that uniquely identify each time entry in the DataFrame.
- description: This column stores the description or details associated with the time entry. It likely contains text values representing a description of the activity or task performed during the time entry.
- tagIds: This column stores the identifiers or unique identifiers of the tags associated with the time entry. It likely contains a list or nested data structure that indicates the tags associated with the time entry.
- userId: This column represents the identifier or unique identifier of the user who created the time entry. It likely contains alphanumeric values that uniquely identify the user.
- billable: This column indicates whether the time entry is billable or not. It likely contains boolean values (True or False), with True indicating that the time entry is billable and False indicating that it is not.
- taskId: This column stores the identifier or unique identifier of the task associated with the time entry. It likely contains alphanumeric values that uniquely identify the task.
- projectId: This column represents the identifier or unique identifier of the project associated with the time entry. It likely contains alphanumeric values that uniquely identify the project.
- timeInterval_start: This column stores the start timestamp of the time interval for the time entry. It likely contains timestamp values indicating when the time entry started.
- timeInterval_end: This column stores the end timestamp of the time interval for the time entry. It likely contains timestamp values indicating when the time entry ended.
- timeInterval_duration: This column stores the duration of the time entry. It likely contains a time duration format, such as "PT37M16S" (indicating a duration of 37 minutes and 16 seconds).
- workspaceId: This column represents the identifier or unique identifier of the workspace associated with the time entry. It likely contains alphanumeric values that uniquely identify the workspace.
- isLocked: This column indicates whether the time entry is locked or not. It likely contains boolean values (True or False), with True indicating that the time entry is locked and False indicating that it is not.
- customFieldValues: This column stores custom field values associated with the time entry. It likely contains nested data structures or lists that hold custom field values specific to the time entry.
- type: This column indicates the type or category of the time entry. It likely contains text values representing the type of activity or task associated with the time entry.
- kioskId: This column stores the identifier or unique identifier of the kiosk associated with the time entry. It likely contains alphanumeric values that uniquely identify the kiosk.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Time-entry/operation/getTimeEntries)
- [Clockify API Client](https://github.com/toggl/clockify-api-python)

## Input

### Import libraries


```python
import requests
import naas
import pandas as pd
```

### Setup Variables
- `api_key`: [Get your API key](https://clockify.me/user/settings)
- `workspace_id`: ID of the workspace
- `user_id`: ID of the user to get time entries from

For more information on how to get the workspace and user ID, please refer to [this documentation](https://docs.clockify.me/#operation/getWorkspaces).


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
user_id = "5e1c633abff57e6a72cd8000"
```

## Model

### Get time entries

This function will get all time entries for a user on a workspace.


```python
def get_time_entries(workspace_id, api_key, user_id):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/user/{user_id}/time-entries"
    headers = {"X-Api-Key": api_key}
    response = requests.get(url, headers=headers)
    return response.json()

time_entries = get_time_entries(workspace_id, api_key, user_id)
print("Time entries fetched:", len(time_entries))
```

### Flatten nested dict


```python
# Flatten the nested dict
def flatten_dict(d, parent_key='', sep='_'):
    """
    Flattens a nested dictionary into a single level dictionary.

    Args:
        d (dict): A nested dictionary.
        parent_key (str): Optional string to prefix the keys with.
        sep (str): Optional separator to use between parent_key and child_key.

    Returns:
        dict: A flattened dictionary.
    """
    items = []
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.extend(flatten_dict(v, new_key, sep=sep).items())
        else:
            items.append((new_key, v))
    return dict(items)

df_time_entries = pd.DataFrame()
for time_entry in time_entries:
    res = flatten_dict(time_entry)
    tmp_df = pd.DataFrame([res])
    df_time_entries = pd.concat([df_time_entries, tmp_df])
    
df_time_entries = df_time_entries.reset_index(drop=True)
print("Time entries fetched:", len(df_time_entries))
```

## Output

### Display result


```python
df_time_entries
```

 
