<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Clockify/Clockify_Find_tasks_on_project.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Clockify+-+Find+tasks+on+project:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #clockify #task #project #find #api #python

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook will help you find tasks on a project using Clockify API. It will return a dataframe with columns as follow:
- id: This column stores an identifier or unique identifier associated with a task. It likely contains alphanumeric values that uniquely identify each task in the DataFrame.
- name: This column stores the names or titles associated with the tasks. It likely contains text values representing the names or titles of the tasks.
- projectId: This column represents the identifier or unique identifier of the project to which each task belongs. It likely contains alphanumeric values that uniquely identify the project.
- assigneeIds: This column stores the identifiers or unique identifiers of the assignees assigned to the tasks. It likely contains a list or nested data structure that indicates the assignees associated with each task.
- assigneeId: This column stores the identifier or unique identifier of a single assignee assigned to the task. It likely contains a single value indicating the assignee for the task.
- userGroupIds: This column stores the identifiers or unique identifiers of the user groups associated with the tasks. It likely contains a list or nested data structure that indicates the user groups associated with each task.
- estimate: This column stores the estimate or estimated duration for each task. It likely contains a time duration format, such as "PT0S" (indicating zero duration).
- status: This column indicates the status of the tasks, whether they are active or inactive. It likely contains text values such as "ACTIVE" or "INACTIVE".
- duration: This column stores the actual duration or time taken for each task. It likely contains a time duration format, such as "PT2H42M1S" (indicating a duration of 2 hours, 42 minutes, and 1 second).
- billable: This column indicates whether the task is billable or not. It likely contains boolean values (True or False), with True indicating that the task is billable and False indicating that it is not.
- hourlyRate: This column stores the hourly rate associated with the task. It likely contains numerical values representing the rate for the task, such as an hourly billing rate.
- costRate: This column stores the cost rate associated with the task. It likely contains numerical values representing the cost rate for the task, such as the rate at which the task incurs costs.

**References:**
- [Clockify API Documentation](https://docs.clockify.me/#tag/Task/operation/getTasks)
- [Clockify API Client](https://github.com/tomasbasham/clockify-api)

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
- `project_id`: [Find your project ID](https://clockify.me/developers-api#operation/getProjects)


```python
api_key = naas.secret.get("CLOCKIFY_API_KEY") or "YOUR_API_KEY"
workspace_id = "626f9e3b36c2670314c0386e" #"<WORKSPACE_ID>"
project_id = "637e3121e9eca632b62aee58"
```

## Model

### Find tasks on project


```python
def get_tasks(api_key, workspace_id, project_id):
    url = f"https://api.clockify.me/api/v1/workspaces/{workspace_id}/projects/{project_id}/tasks"
    headers = {"X-Api-Key": api_key}
    response = requests.get(url, headers=headers)
    return response.json()

tasks = get_tasks(api_key, workspace_id, project_id)
```

## Output

### Display result


```python
print("Tasks found:", len(tasks), "\n")
for task in tasks:
    print("-", task["name"], f'(id: {task["id"]})')

df = pd.DataFrame(tasks)
df
```

 
