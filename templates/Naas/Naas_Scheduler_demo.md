# Scheduler demo

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/Open\_in\_Naas\_Lab.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Scheduler\_demo.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=Naas+-+Scheduler+demo:+Error+short+description) | [Generate Data Product](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Start\_data\_product.ipynb)

**Tags:** #naas #scheduler #snippet #operations

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

Transform all your work routines in notebooks and run them even when you sleep.\
Here we are going to use the Notifications feature to test Scheduler.

📺 Start learning how to schedule your Naas notebook on our [Youtube channel](https://www.youtube.com/channel/UCKKG5hzjXXU\_rRdHHWQ8JHQ?sub\_confirmation=1).\


```python
from IPython.display import IFrame

IFrame(src="https://www.youtube.com/embed/ONiILHFItzs", width="560", height="315")
```

Read the doc: https://naas.gitbook.io/naas/features/scheduler

### Input

#### Import library

```python
import naas
from IPython.display import HTML
```

#### Setup Naas notification

```python
# Email receiver
EMAIL_TO = "ENTER_YOUR_EMAIL_TO_HERE"  # EXAMPLE: "hello@naas.ai"

# Email subject
EMAIL_SUBJECT = "Naas Scheduler Test"
```

#### Setup Naas scheduler

```python
# Schedule your notebook everyday at 9:00 AM
naas.scheduler.add(cron="0 9 * * *")

# To delete your scheduler, uncomment the line below and execute this cell
# naas.scheduler.delete()
```

### Model

#### Create content

```python
# Email content
EMAIL_CONTENT = """
<p>Hello !</p>
<p>If i put html in there..&nbsp;</p>
<p><img src="https://specials-images.forbesimg.com/imageserve/5f1f37a40a5db2c8275972c0/960x0.jpg?fit=scale" alt="" width="959" height="663" /></p>
"""

# Display content
HTML(EMAIL_CONTENT)
```

#### Send the email

```python
result = naas.notification.send(
    email_to=EMAIL_TO, subject=EMAIL_SUBJECT, html=EMAIL_CONTENT
)
```

### Output

#### Display result

```python
result
```
