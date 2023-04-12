<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Automate_GitHub_Auth.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Automate+GitHub+Auth:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #asset #snippet #operations

**Author:** [Jeremy Ravenel](https://www.linkedin.com/in/ACoAAAJHE7sB5OxuKHuzguZ9L6lfDHqw--cdnJg/)

**Description:** This notebook provides an automated way to authenticate with GitHub using Naas.

## Input

No input required.

## Model
Generate the public key:


```python
!ssh-keygen -b 2048 -t rsa -f /home/ftp/.ssh/id_rsa -q -N ""
```

## Output

Retrieve the public key by running the cell below:


```python
cat /home/ftp/.ssh/id_rsa.pub
```

Then: 
- go Github/Settings/SSH and GCP keys
- create new SSH key
- paste the public key in the key section
- name the public key and save

You just changed the way naas connects with GitHub for any repository. <br>
It means you need to choose the SSH method to clone now but you can still use Git tab to push.

- Click on File > New > Terminal 
- Type : git clone git@github.com:jravenel/my_project.git

This technique wil enable you to never use your Git username and password anymore.
